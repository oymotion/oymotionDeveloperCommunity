# ROHDemoCollection  Suitable for ROH-A001/A002, ROH-LiteS001, ROH-AP001/AP002

## Demo Acquisition

- Windows: Download [Volume 1 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_windows.zip), [Volume 2 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_windows.z01), [Volume 3 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_windows.z02), [Volume 4 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_windows.z03), [Volume 5 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_windows.z04), place them in the same directory and unzip them  

- Ubuntu(22.04): Download [Volume 1 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_ubuntu.zip), [Volume 2 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z01), [Volume 3 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z02), [Volume 4 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z03), [Volume 5 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_ubuntu.z04), place them in the same directory and unzip them  

- Jetson: Download [Volume 1 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_jetson.zip), [Volume 2 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_jetson.z01), [Volume 3 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_jetson.z02), [Volume 4 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_jetson.z03), [Volume 5 of the compressed package](../../../assets/downloads/ROHand/DemoCollection_jetson.z04), place them in the same directory and unzip them  

## Demo Introduction

ROHand's ROHDemoCollection is developed based on Python pyqt6, Below is the demo introduction:  

- Currently supported ROHand models include ROH-A001/A002, ROH-LiteS001, ROH-AP001/AP002.  

- The Demo currently offers three control methods: vision control, glove control, gForce myoelectric armband control, loop test, and action sequence control.  

### Install CH341SER Driver

[Click here](../../../assets/downloads/ROHand/CH341SER.EXE) to download CH341SER driver  

Double-click the exe file to open the CH341SER installer  

Click Install to proceed  

### Run Method

- Windows: Double-click to run  

- Ubuntu:  
  - 1. Give the required port permissions, such as `sudo chmod 666 /dev/ttyUSB0`  
  - 2. Run the program, `./RohDemoCollection_xxxxx` xxxxx is the software version number  

- Jetson: 
  - 1. Give the required port permissions, such as `sudo chmod 666 /dev/ttyCH341USB0`  
  - 2. Run the program, `./RohDemoCollection_xxxxx` xxxxx is the software version number  

For usage details, please visit the [UserGuide](../../../assets/downloads/ROHand/ROHDemoCollection_UserGuide_en.pdf){: target="_blank"}