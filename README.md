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

