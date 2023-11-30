# My 3DP Configs
[![Build Status](https://github.com/macdylan/3dp-configs/actions/workflows/pack.yml/badge.svg)]
[English Readme](./README-en.md)

非官方的 PrusaSlicer 和 OrcaSlicer 打印参数，由我个人标定，请仔细阅读子目录下的 README 进行正确配置。如果遇到打印错误，请提出 Issue，感谢：）

> 受限于可测试的材料和打印环境差异，在投入使用前请务必进行打印验证和相关的耗材校准

## 安装使用

请先下载你需要的配置包：[Releases](https://github.com/macdylan/3dp-configs/releases)

我会经常更新它们，由于是非官方配置文件，它们无法在软件中自动更新，请手动下载安装。同时我也在积极的与这些项目的维护者联系，尽快合并到软件的发行版中去。


### PrusaSlicer

- 打开 PrusaSlicer，点击 `Help` 菜单 / `Show Configuration Folder`
- 解压缩配置包的 zip 文件，将所有文件复制到 `vendor` 目录下，如果目标文件已存在，选择覆盖
- 重新启动 PrusaSlicer，点击 `Configuration` 菜单 / `Configuration Assistant(or Wizard)`
- 从 Other Vendors 中选择 Snapmaker，点击 Next，选择需要的打印机和耗材，然后完成设置向导

### OrcaSlicer

> 请注意，如果你使用发行版中的 Snapmaker 参数，并另存了修改的设置，它们将会消失（不是丢失，仍会保存在你的个人文件夹中，但是不会显示在菜单中）

- 打开 OrcaSlicer，在 Printer 中取消之前配置过的 Snapmaker 设备，然后关闭软件
- 进入程序安装目录：
  - macOS: /Applications/OrcaSlicer.app/Contents/Resources/profiles/
  - win: （找到程序安装在哪了）/profiles/
- 解压缩配置包的 zip 文件，将所有文件复制进去，选择覆盖
- 重新启动 OrcaSlicer，在 `Printer` 中添加 Snapmaker 打印机，然后在 `Filament` 中添加 Snapmaker 的所有新耗材，完成。

### 连接 Snapmaker 打印机

需要使用我的另一个项目 [sm2uploader](https://github.com/macdylan/sm2uploader)，它模拟了 OctoPrint 的服务接口，因此你可以使用软件中的物理打印机连接功能，将切片通过 sm2uploader 中转发送到 Snapmaker 打印机。

<img width="701" src="./_assets/3.png">
<br />
<img width="701" src="./_assets/4.png">


## 关于 Start GCodes 的逻辑说明

在 20231130 版本中，增加了清理喷嘴的一些逻辑，完整的动作步骤如下：

1. 开启热床首层温度，同时预热喷嘴到 165 度，并将喷嘴移动到方便进行手动清理的位置。你可以观察喷嘴周围的污染情况，并使用钢丝刷或其它工具处理
2. 热床到达目标温度后，喷嘴位置归零。如果是 Snapmaker 2 设备，会在 0.2mm 高度环绕热床一圈进行机构检查，你可以观察热床是否基本平整，此外也可以观察喷嘴运行的边界，因为双挤出机+QuickSwapKit会缩小可运动的范围；如果是 J1，只会闪动 LED 提示即将归零执行头，没有其它动作
3. 喷嘴回到热床外，升温到打印温度之上的 15 度。目的是为了避免喷嘴里残留有其它高温材料造成无法挤出，请注意这个温度是我的经验值，如果你遇到堵头请提出 issue
4. 进行两段不同温度的耗材冲刷，确保喷嘴更加干净。总共大约使用 4-8cm 的耗材，没有太多的浪费，我认为可靠的打印是更重要的。如果你不想有任何浪费，可以在 gcode 中使用 `{if 0 == 1}...{endif}` 来关闭这段逻辑
5. 如果你使用双挤出机模组或J1进行双材料打印，会预先冲刷将要待机的喷嘴，再冲刷初始打印的喷嘴。我希望实际打印时不会出现错误的装料或喷嘴故障，所以任何预先的检查都是必要的
6. 冲刷后会在热床边缘挤出一条 L 形的细线，这将沾走喷嘴周围的残留，对提升打印质量会有帮助
7. 正式开始打印
8. 打印结束时，将耗材回抽到挤出轮附近，即便冷却后，你也可以方便的更换耗材而无需剪断或者加热

其中的一些逻辑会因为设备类型的不同而有区别。如果你认为这个项目对你有所帮助，请点击 Github 右上角的 Star 给予支持。或许也可以请我喝杯咖啡，非常感谢：https://ko-fi.com/L3L1MFQF6
