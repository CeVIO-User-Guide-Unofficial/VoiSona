原文：<https://manual.voisona.com/en/talk/pc/2b6e9bc7efb18014b922c93fcaa8aac4>

---

# REST API 教程

## 什么是 REST API

REST API（Representational State Transfer Application Programming Interface）是一种允许外部程序访问应用程序功能的接口。它通过 HTTP 请求和响应进行通信，使您可以自动执行语音合成请求、检查状态和获取结果等任务。

通过在 VoiSona Talk 中启用 REST API，您可以从 Python、C++ 或 JavaScript 等各种编程语言控制语音合成。这使得将 VoiSona Talk 的合成语音集成到您自己的应用程序、Web 服务、聊天机器人或游戏中成为可能。

在以下教程中，我们将逐步介绍如何在 VoiSona Talk 中启用 REST API，并使用 Python 执行语音合成。

*REST API 功能目前作为测试版提供。

---

## 启用 REST API

1. 启动 VoiSona Talk。
2. 如果尚未认证，请先进行认证：
   1. 从右上角的 ☰（三线菜单）中，选择「帮助」→「登录」。
   2. 邮箱：输入您注册的电子邮箱地址。
   3. 密码：输入您注册时设置的密码。
3. 确保至少已下载一个声库。
4. 启用 REST API：
   1. 从右上角的 ☰（三线菜单）中，选择「编辑」→「环境设置」，打开「API」标签页。
   2. 为 API 监听器设置任意端口号（默认值：32766）。
   3. 确认用户名与您注册的电子邮箱地址一致（此字段无法更改）。
   4. 设置您选择的 API 密码。此密码无需与登录密码相同。但不能为空。
   5. 勾选「启用 REST API」。启用后，端口号和密码字段将变为只读。如需更改，请取消勾选，修改值后重新启用。
   6. 启用后，复选框旁边的「Talk API 参考」链接将变为可用。可参考它获取更详细的 API 规范。

---

## 示例：使用 Python 调用 API

### 完整示例代码

以下是完整的示例代码。每个部分将在后续章节中详细说明。

```python
import argparse
import json
import os
import sys
import time
import xml.etree.ElementTree as ET
import requests

parser = argparse.ArgumentParser()
parser.add_argument("--user", type=str, required=True, help="用户名")
parser.add_argument("--password", type=str, required=True, help="API 密码")
parser.add_argument("--port", type=int, default=32766, help="端口号")
parser.add_argument("--output-wav", type=str, default="test.wav", help="WAV 文件名")
args = parser.parse_args()

auth = (args.user, args.password)
base_url = f"http://localhost:{args.port}/api/talk/v1/"

def get_voice_libraries():
    """获取可用声库列表"""
    response = requests.get(base_url + "voices", auth=auth)
    response.raise_for_status()
    voice_libraries = response.json()["items"]
    print("以下是可用声库列表：")
    print(json.dumps(voice_libraries, indent=2, ensure_ascii=False))
    return voice_libraries

def synthesize_text(voice_library):
    """提交语音合成请求"""
    payload = {
        "text": "こんにちは",
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
        "force_enqueue": True,
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    uuid = response.json()["uuid"]
    print("请求已成功发送。")
    return uuid

def check_status(uuid, synth=True, timeout=30):
    """检查请求处理状态"""
    start = time.time()
    endpoint = "speech-syntheses" if synth else "text-analyses"
    while True:
        response = requests.get(base_url + endpoint + "/" + uuid, auth=auth)
        response.raise_for_status()
        state = response.json()["state"]
        if state == "succeeded":
            break
        if time.time() - start > timeout:
            raise TimeoutError("处理超时。")
        time.sleep(0.1)
    print("请求处理完成。")
    return response

def delete_request(uuid):
    """删除请求"""
    response = requests.delete(base_url + "speech-syntheses/" + uuid, auth=auth)
    response.raise_for_status()
    print("请求已删除。")

def synthesize_text_and_save(voice_library):
    """合成语音并保存为文件"""
    payload = {
        "text": "こんにちは",
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
        "can_overwrite_file": True,
        "destination": "file",
        "output_file_path": os.path.abspath(args.output_wav),
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    uuid = response.json()["uuid"]
    print("请求已成功发送。")
    return uuid

def synthesize_text_with_global_parameters(voice_library):
    """使用全局参数合成语音"""
    payload = {
        "text": "こんにちは",
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
        "global_parameters": {
            "alp": 0.0,
            "huskiness": 0.0,
            "intonation": 1.0,
            "pitch": 0.0,
            "speed": 2.0,
            "style_weights": [],
            "volume": 0.0,
        },
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    uuid = response.json()["uuid"]
    print("请求已成功发送。")
    return uuid

def analyze_text():
    """分析文本"""
    payload = {
        "text": "こんにちは",
        "language": "ja_JP",
    }
    response = requests.post(base_url + "text-analyses", auth=auth, json=payload)
    uuid = response.json()["uuid"]
    response = check_status(uuid, synth=False)
    analyzed_text = response.json()["analyzed_text"]
    print("文本分析完成。")
    print(analyzed_text)
    return analyzed_text

def synthesize_text_with_analyzed_text(voice_library, analyzed_text):
    """使用分析后的文本合成语音"""
    root = ET.fromstring(analyzed_text)
    word = root.find(".//word")
    word.set("hl", "hllll")
    word.set("pronunciation", "コンニチハ")
    modified_analyzed_text = ET.tostring(root, encoding="unicode")
    print(modified_analyzed_text)
    payload = {
        "analyzed_text": modified_analyzed_text,
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    uuid = response.json()["uuid"]
    print("请求已成功发送。")
    return uuid

try:
    voice_libraries = get_voice_libraries()
    if len(voice_libraries) == 0:
        print("请先下载声库。")
        sys.exit(1)

    voice_library = voice_libraries[0]

    uuid = synthesize_text(voice_library)
    check_status(uuid)
    delete_request(uuid)

    uuid = synthesize_text_and_save(voice_library)
    check_status(uuid)
    time.sleep(2)  # 等待之前的音频播放完毕

    uuid = synthesize_text_with_global_parameters(voice_library)
    check_status(uuid)
    time.sleep(2)  # 等待之前的音频播放完毕

    analyzed_text = analyze_text()
    uuid = synthesize_text_with_analyzed_text(voice_library, analyzed_text)
    check_status(uuid)

    print("教程已顺利执行完成，没有出现错误。")

except requests.exceptions.ConnectionError as e:
    print("连接失败。请检查服务器状态和配置。")
    print(e)
except requests.exceptions.HTTPError as e:
    print("发生 HTTP 错误。")
    print(e)
except Exception as e:
    print("发生意外错误。")
    print(e)
```

要运行示例代码，您需要安装 `requests` 包：

```bash
pip install requests
```

运行示例的命令示例：

```bash
python sample.py --user hoge@example.com --password 1234
```

请根据您的 API 设置替换用户名和密码。

---

### 获取可用声库

可以按如下方式获取已安装声库的列表：

```python
auth = (args.user, args.password)
base_url = f"http://localhost:{args.port}/api/talk/v1/"

def get_voice_libraries():
    response = requests.get(base_url + "voices", auth=auth)
    response.raise_for_status()
    voice_libraries = response.json()["items"]
    print("以下是可用声库列表：")
    print(json.dumps(voice_libraries, indent=2, ensure_ascii=False))
    return voice_libraries
```

示例输出：

```json
[
  {
    "display_names": [
      {
        "language": "ja_JP",
        "name": "田中傘"
      },
      {
        "language": "en_US",
        "name": "Tanaka San"
      }
    ],
    "languages": [
      "ja_JP"
    ],
    "voice_name": "tanaka-san_ja_JP",
    "voice_version": "2.0.0"
  }
]
```

如果编辑器中未下载任何声库，结果将为空。

---

### 合成语音

以下代码向 API 服务器发送语音合成请求：

```python
def synthesize_text(voice_library):
    payload = {
        "text": "こんにちは",
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
        "force_enqueue": True,
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    uuid = response.json()["uuid"]
    print("请求已成功发送。")
    return uuid
```

在示例代码中，将从获取到的声库列表中使用第一个检测到的声库作为合成用声库。合成完成后，您将听到通过默认音频设备播放的「こんにちは」。

请注意，服务器对请求数量有限制。如果达到限制，请求可能会失败。设置 `force_enqueue: true` 会自动删除较旧的请求以为新请求腾出空间。

您可以使用执行 `synthesize_text` 函数获得的 UUID 来查询已提交请求的状态：

```python
def check_status(uuid, timeout=30):
    start = time.time()
    while True:
        response = requests.get(base_url + "speech-syntheses/" + uuid, auth=auth)
        response.raise_for_status()
        state = response.json()["state"]
        if state == "succeeded":
            break
        if time.time() - start > timeout:
            raise TimeoutError("处理超时。")
        time.sleep(0.1)
    print("请求处理完成。")
    return response
```

如果 `state` 为 `queued`，表示请求正在等待处理。如果为 `succeeded`，表示合成已成功完成。

也可以使用 UUID 删除请求：

```python
def delete_request(uuid):
    response = requests.delete(base_url + "speech-syntheses/" + uuid, auth=auth)
    response.raise_for_status()
    print("请求已删除。")
```

要将合成结果保存为文件而不是播放，请指定绝对路径：

```python
def synthesize_text_and_save(voice_library):
    payload = {
        "text": "こんにちは",
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
        "can_overwrite_file": True,
        "destination": "file",
        "output_file_path": os.path.abspath(args.output_wav),
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    print("请求已成功发送。")
```

---

### 控制语音表现力

要修改语音表现力，请包含 `global_parameters` 对象。例如，将语速加倍：

```python
def synthesize_text_with_global_parameters(voice_library):
    payload = {
        "text": "こんにちは",
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
        "global_parameters": {
            "alp": 0.0,       # 声质
            "huskiness": 0.0, # 沙哑度
            "intonation": 1.0, # 语调
            "pitch": 0.0,     # 音高
            "speed": 2.0,     # 语速（2.0 = 两倍速）
            "style_weights": [], # 风格权重
            "volume": 0.0,    # 音量
        },
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    print("请求已成功发送。")
```

---

### 语音属性的详细控制

可以通过修改分析后的文本数据来进行精细控制。首先发送文本分析请求：

```python
def analyze_text():
    payload = {
        "text": "こんにちは",
        "language": "ja_JP",
    }
    response = requests.post(base_url + "text-analyses", auth=auth, json=payload)
    uuid = response.json()["uuid"]
    response = check_status(uuid, synth=False)
    analyzed_text = response.json()["analyzed_text"]
    print("文本分析完成。")
    print(analyzed_text)
    return analyzed_text
```

示例响应（XML 格式）：

```xml
<tsml><acoustic_phrase><word chain="0" hl="lhhhh" original="こんにちは"
phoneme="k,o|N|n,i|ch,i|w,a" pos="感動詞" pronunciation="コンニチワ">
こんにちは</word></acoustic_phrase></tsml>
```

通过修改分析后的文本并将其发送回服务器，可以调整重音和发音。以下是使用 XML 解析器的示例：

```python
def synthesize_text_with_analyzed_text(voice_library, analyzed_text):
    root = ET.fromstring(analyzed_text)
    word = root.find(".//word")
    word.set("hl", "hllll")           # 修改重音模式
    word.set("pronunciation", "コンニチハ")  # 修改发音
    modified_analyzed_text = ET.tostring(root, encoding="unicode")
    print(modified_analyzed_text)
    payload = {
        "analyzed_text": modified_analyzed_text,
        "language": voice_library["languages"][0],
        "voice_name": voice_library["voice_name"],
        "voice_version": voice_library["voice_version"],
    }
    response = requests.post(base_url + "speech-syntheses", auth=auth, json=payload)
    response.raise_for_status()
    print("请求已成功发送。")
```

有关更多详细信息，请通过 VoiSona Talk 编辑器「环境设置」窗口的「API」标签页中的链接参阅「Talk API 参考」。
