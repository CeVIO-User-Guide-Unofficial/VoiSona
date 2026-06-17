原文：<https://manual.voisona.com/ja/song/pc/2b6e9bc7efb1802fa1c0e3bb3223e086>

---

# 调整参数

在 VoiSona 中，从影响整首歌曲的参数调整，到时机和颤音等细节调整，都得到了广泛支持。

## 调整整首歌曲的参数

每个轨道都可以调整影响整首歌曲的参数。

1. 点击「参数」按钮，显示面板。
2. 直接输入数值或使用滑块进行调整。
   ![全局参数面板](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-80a3-8604-d14fbe2925a1/242bdf56771349afe84b59dd275eadcb.png)

!!! info "可调整的参数"

      - TUNE（精准音高）：与音符音高的相符程度。数值越低，离音符音高越远；数值越高，越接近音符音高。
      - VIA（颤音幅度）：颤音的幅度。数值越大，振幅越大。
      - VIF（颤音频率）：颤音的频率。数值越大，周期越短、越细密。
      - ALP（音色/声质）：声音的音色/质感。数值越小越像小孩，数值越大越像大人。
      - HUS（沙哑度）：声音的沙哑程度。数值越大，声音越沙哑。

---

## 更详细的参数调整

切换调整画面，可以进行更详细的参数设置。各参数的调整画面可通过标签页切换，标签页的显示或隐藏也可自由设置。

### 调整时机

可以调整音素开始或结束的时机。

1. 点击「TMG」显示调整画面。
2. 选择「钢笔工具」或「线条工具」。
3. 拖动状态线。
   ![时机调整](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8026-979d-cbdf40c633af/7ddaf5e6f3492f8cc45b71ce452487a2.png)

---

#### 以更细粒度调整

在「环境设置」的「编辑器」标签页中，勾选「时机状态线」。这样会将音素进一步分为 5 个部分显示线条，可以进行更精细的时机调整。

!!! info
      在比音素更细的粒度上调整时机，效果可能不太明显。
      ![细粒度时机](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8086-a8cd-e21248c55152/6e79812a3cb2cb4069ab1536294c07aa.png)

---

#### 将元音校正到音符开头

使用「选择工具」指定范围后，右键点击选择「元音时间修正」。这样会将线条自动调整，使元音位于音符开头。

![元音时间修正](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8027-be33-c8161bc99526/a7521da96f642409bae9b8c7c65645ee.png)

---

### 调整其他参数

其他参数也可以轻松自由地调整。

1. 点击「VOL」「PIT」「ALP」「HUS」之一显示调整画面。
2. 选择「钢笔工具」或「线条工具」。
3. 绘制线条。
   ![参数绘制](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-80bf-bef7-ffd42a998cc2/c10267ea1dfd024c3280a3cad8dc3bb2.png)

!!! info "可调整的参数"
      - VOL（音量）：单位是 dB（分贝）。
      - PIT（音高）：单位是 Hz（赫兹）。
      - ALP（音色/声质）：数值越小越像小孩，数值越大越像大人。
      - HUS（沙哑度）：数值越大，声音越沙哑。

---

#### 复制参数线条

要复制参数线条，使用「选择工具」选择范围后，执行以下任一操作：

- 仅复制自己绘制的线条：复制后，使用播放位置光标指定位置，然后粘贴。
  ![复制线条](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8066-858e-f505d306f257/74f8b18ad94ce91de1e10d888c9ce406.png)
- 复制原始线条和自己绘制的线条：上下拖动范围内的线条。自己绘制线条的部分会被覆盖，其他部分则直接复制原始参数线条。
  ![拖动复制](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-80e9-8798-d880f343fe24/7c73365f806cb22dca5d988dc3454665.png)

---

#### 禁用参数效果

在 PIT 和 VIB（Detailed 模式）中，可以禁用已绘制参数的效果。按住 <kbd>Shift</kbd> 键的同时使用「橡皮擦工具」拖动原本设置的参数线条，线条将变为白色，该部分的参数将被禁用。

!!! info
      禁用部分的效果如下：
      - PIT：失去音高，变为沙哑的歌声。
      - VIB：没有颤音，变为平坦的歌声。

![禁用参数](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8011-a7f0-d67bd6acc1ee/7403c5f75275bdddcde6e230660f4239.png)

---

#### 连接调整模式

调整音高、音量和颤音时，按住 <kbd>Alt</kbd> 键拖动，可以绘制平滑连接到原始值的线条。按住 <kbd>Alt</kbd> 键拖动时会绘制红色线条，松开 <kbd>Alt</kbd> 键后，红色线条与原始线条的连接点之间的部分将反映为调整值。按住 <kbd>Alt</kbd> 键期间会显示反映调整值的单线画面，方便确认有效值。

![连接调整1](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/2e1e9bc7-efb1-80cb-bb64-e0578872b139/5b4c86374f4ae138baf87ac8101fd5ea.png)
![连接调整2](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/2e1e9bc7-efb1-80a3-a692-c16140d99aea/039449e5470dfeaece9400ccdbbdc121.png)

---

### 颤音调整

可以添加新的颤音，或调整振幅和周期。提供两种模式，可在直观操作（Simplified 模式）和自由编辑（Detailed 模式）之间切换。

1. 点击「VIB」显示调整画面。
2. 选择「钢笔工具」或「线条工具」。
3. 编辑颤音区间。默认是 Simplified 模式，可进行以下操作：
    - 新建：绘制线条时将自动创建新的框。
    - 调整开始/结束位置：光标对准框的边缘，变为箭头后左右拖动。
    - 调整振幅：光标对准框，变为箭头后上下拖动。
    - 调整频率：从框内向外左右拖动。
      ![颤音调整](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8071-9cb7-d58b9d6c80bc/ce74c6f903b97181d2a4ccbed764f169.png)

!!! info "关于振幅与频率"
      - 振幅：单位是 Cent（音分），100 Cent 相当于上下半音。数值越大，波的上下振幅越大。
      - 频率：单位是 Hz（赫兹），表示每秒波振动的次数。数值越大，波越细密（振幅间隔越短）。

---

#### 更自由的调整（Detailed 模式）

点击钢琴卷帘右上角的「Detailed」按钮切换模式。画面将分为上下两部分，上方的「Amp.」可自由调整振幅，下方的「Frq.」可自由调整周期。基本操作与[调整其他参数](#_7)相同，但在其中一个画面中添加或删除线条时，另一个画面也会自动反映。

![Detailed模式](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-80de-8b16-d8bb00e001ea/2558de1efffe49055fec37d115ae9d3d.png)

---

### 批量选择音符和参数

使用「批量选择工具」，可以同时选择音符和参数。这样移动、复制、删除等操作都可以批量进行。

1. 选择「批量选择工具」。
2. 左右拖动，使音符和参数包含在选中范围内。
   ![批量选择](https://s3.ap-northeast-1.amazonaws.com/wraptas-prod/voisona-manual/348e9bc7-efb1-8024-947a-ccccc4646fa8/eeb74f3554dc539e385e20e28d57c345.png)
