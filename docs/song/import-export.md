原文：[ファイルをインポート・エクスポートする](https://manual.voisona.com/ja/song/pc/2b6e9bc7efb1807daf26f729d3dac3a9)

---

# 导入与导出文件

可以读取 VoiSona 或其他应用程序创建的文件，也可以将编辑中的数据导出。

## 导入文件

可以导入其他项目或其他应用程序创建的文件。

!!! info "可导入的文件格式"
      - CCS：以 CeVIO Creative Studio、CeVIO AI 的项目为单位保存的文件。当有多个轨道时可以选择要读取的轨道。
      - CCST：以 CeVIO Creative Studio、CeVIO AI 的轨道为单位保存的文件。
      - MIDI：MIDI 格式的音乐数据文件。当有多个轨道时可以选择要读取的轨道。
      - Music XML：Music XML 格式的乐谱数据文件。
      - tssprj：VoiSona 独有的项目文件格式。
      - tsmsln：iOS/iPadOS 版 VoiSona 独有的项目文件格式。
      - UST：UTAU 的歌唱数据文件。

### 在独立应用中导入

在独立应用中，可以将文件导入到选中的轨道或新轨道，然后在编辑器上编辑和播放。

1. 选择以下操作之一：
    - 导入到选中轨道：在轨道上右键点击选择「读取文件」
      ![读取文件](images/song_import-export_Importing_and_Exporting_Files_4.png)
    - 导入到新轨道：菜单栏的「文件」>「导入」
      ![文件导入菜单](images/song_import-export_Importing_and_Exporting_Files_5.png)
2. 选择文件并点击「打开」。文件内容将导入到选中的轨道或新轨道中。

!!! info
      选择 MIDI 文件、CCS 文件时，会显示导入设置画面。

---

### 在插件中导入

在插件中，可以将文件导入到选中的轨道，然后在编辑器上编辑和播放。

1. 点击「菜单」按钮，选择「导入」。
2. 选择文件并点击「打开」。选中轨道中将导入文件内容。
   ![插件导入](images/song_import-export_Importing_and_Exporting_Files_0.png)

!!! info
      选择 MIDI 文件、CCS 文件时，会显示导入设置画面。

---

## 读取音频文件

在独立应用中使用时，可以将音频文件读取到音频轨道。

1. 在音频轨道的时间轴上右键点击，点击「读取音频文件」。
   ![读取音频](images/song_import-export_Importing_and_Exporting_Files_1.png)
2. 选择文件并点击「打开」。此时将读取音频文件。
   ![读取完成](images/song_import-export_Importing_and_Exporting_Files_2.png)

!!! info
      也可以通过将文件拖放到时间轴上的方式来读取。

---

## 从 DAW 传输 MIDI

在乐器插件中使用时，可以将 DAW 中输入的 MIDI 信息传输到 VoiSona。

1. 在 DAW 侧准备与 VoiSona 同一轨道的 MIDI 信息。
2. 在 VoiSona 编辑画面中打开「Transfer」按钮。
   ![Transfer按钮](images/song_import-export_Importing_and_Exporting_Files_8.png)
3. 在 DAW 侧开始播放。
   ![DAW播放](images/song_import-export_Importing_and_Exporting_Files_9.png)
4. 待需要传输的区间全部播放完毕后，停止播放。传输完成。
   ![传输完成](images/song_import-export_Importing_and_Exporting_Files_3.png)

!!! info
      只有播放区间的 MIDI 信息会反映到 VoiSona 中。

---

## 导出文件

导出文件后，可以在其他项目或其他应用程序中使用。

1. 选择以下操作之一：
    - 独立应用：菜单栏的「文件」>「导出」> 选择要导出的文件格式
      ![独立应用导出](images/song_import-export_Importing_and_Exporting_Files_6.png)
    - 乐器插件、ARA 插件：点击「菜单」按钮后选择「导出」> 选择要导出的文件格式
      ![插件导出菜单](images/song_import-export_Importing_and_Exporting_Files_7.png)
2. 在对话框中进行必要的设置后确认。文件将保存到指定位置。

!!! info "文件格式与输出方式"
      - 混音 WAV 导出：将所有轨道合成为一个 WAV 格式文件输出。
      - CCS：CeVIO Creative Studio、CeVIO AI 的项目文件。将所有轨道合成为一个文件输出。
      - MIDI：MIDI 格式的音乐数据文件。将所有轨道合成为一个文件输出。不会输出调整参数。
      - tsmsln：iOS/iPadOS 版 VoiSona 独有的项目文件。输出选中的轨道。会同时保存为轨道分配的声库。
      - tssprj：VoiSona 独有的项目文件。输出选中的轨道。会同时保存为轨道分配的声库。
      - CCST：CeVIO Creative Studio、CeVIO AI 的轨道文件。输出选中的轨道。
      - MusicXML：Music XML 格式的乐谱数据文件。输出选中的轨道。不会输出调整参数。
      - WAV：合成语音波形。输出选中的轨道。勾选「将时间信息作为文本输出」可同时输出 Lab 文件。
