# ROHDemoCollection  适用于 ROH-A001/A002, ROH-LiteS001, ROH-AP001/AP002

## Demo获取

- Windows系统: 下载 [分卷压缩包1](../../../assets/downloads/ROHand/DemoCollection_windows.zip), [分卷压缩包2](../../../assets/downloads/ROHand/DemoCollection_windows.z01), [分卷压缩包3](../../../assets/downloads/ROHand/DemoCollection_windows.z02), [分卷压缩包4](../../../assets/downloads/ROHand/DemoCollection_windows.z03), [分卷压缩包5](../../../assets/downloads/ROHand/DemoCollection_windows.z04) 放在同一目录下并解压  

- Ubuntu系统(22.04): 下载 [分卷压缩包1](../../../assets/downloads/ROHand/DemoCollection_ubuntu.zip), [分卷压缩包2](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z01), [分卷压缩包3](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z02), [分卷压缩包4](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z03), [分卷压缩包5](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z04) 放在同一目录下并解压  

- Jetson系统: 下载 [分卷压缩包1](../../../assets/downloads/ROHand/DemoCollection_jetson.zip), [分卷压缩包2](../../../assets/downloads/ROHand/DemoCollection_jetson.z01), [分卷压缩包3](../../../assets/downloads/ROHand/DemoCollection_jetson.z02), [分卷压缩包4](../../../assets/downloads/ROHand/DemoCollection_jetson.z03), [分卷压缩包5](../../../assets/downloads/ROHand/DemoCollection_jetson.z04) 放在同一目录下并解压  

## Demo简介

ROHand的ROHDemoCollection是基于python pyqt6开发, 以下为Demo介绍:  

- 当前支持的ROHand的有ROH-A001/A002, ROH-LiteS001, ROH-AP001/AP002.  

- Demo目前有五种控制方式: 视觉控制, 手套控制, gForce肌电臂环, 循环测试, 动作序列.  

### 安装CH341SER驱动

[点击此处](../../../assets/downloads/ROHand/CH341SER.EXE)获取CH341SER驱动  

双击exe打开CH341SER安装程序  

点击安装即可  

### 运行方法

- Windows系统: 双击即可运行  

- Ubuntu系统:  
  - 给需要的端口权限, 如 `sudo chmod 666 /dev/ttyUSB0`  
  - 运行程序, `./RohDemoCollection_xxxxx` xxxxx为软件版本号  

- Jetson系统: 
  - 给需要的端口权限, 如 `sudo chmod 666 /dev/ttyCH341USB0`  
  - 运行程序, `./RohDemoCollection_xxxxx` xxxxx为软件版本号  

使用详情请访问[用户手册](../../../assets/downloads/ROHand/ROHDemoCollection_UserGuide_zh.pdf){: target="_blank"}