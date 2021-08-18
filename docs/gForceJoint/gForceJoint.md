# gForce Joint

August 28th, 2020

***

## Brief

This document tries to guiding how one can use gForce gesture armband with Arduino.
Before continuing, please make sure you have sufficient experience with [Arduino](https://www.arduino.cc/), and [ArduinoIDE](https://www.arduino.cc/en/Main/Software) was installed on your PC.

* [What is Arduino](https://www.arduino.cc/en/Guide/Introduction)
* [How to install ArduinoIDE](https://www.arduino.cc/en/Main/Software)
* [Learn Arduino](https://www.arduino.cc/en/Reference/HomePage)

## gForce Joint Usage

This chapter guides the steps to connect gForce Joint to Arm band. The following names are being used: gForceJoint, gForce, gForceSDKArduino, ArduinoMEGA

* [What is gForce200](../gForce200/gForce200UserGuide.md)
* [What is gForcePro/Pro+](../gForcePro/gForcePro.md)
* [What is gForceSDKArduino](https://github.com/oymotion/gForceSDKArduino)
* [What is ArduinoMEGA](https://www.arduino.cc/en/Main/arduinoBoardMega)

![gForceAndArduino](imgs/gForceAndArduino_En.png)

### Step 1: Import gForceSDKArduino  

* [How to import gForceSDKArduino](https://github.com/oymotion/gForceSDKArduino)

### Step 2: Test communication between gForceJoint and ArduinoMEGA

![gForceJointPC](imgs/gForceJointPC_En.png)

1. Wire gForceJoint with ArduinoMEGA:  in this demo case, gForceJoint is connected to MEGA’s Serial Port #2 (gForceJoint (TX) => MEGA (RX2))
2. Open [gForceJointTest](https://github.com/oymotion/gForceSDKArduino/blob/master/examples/gForceJointTest/gForceJointTest.ino) in ArduinoIDE. Compile and upload to ArduinoMEGA.
3. Open the Serial Port Monitor from ArduinoIDE.
4. Set the serial port monitor with a baud rate of 115200bps.
5. Pair and connect gForce armband to gForceJoint, perform the gestures that’s defined, check if the information printed out in the Serial Port Monitor is correct, and hence make sure the connect between gForceJoint and MEGA works.

## Q&A

> How to wear gForce armband?

If a gForce-100/gForce-200 is used, users should follow [wearing instruction](https://oymotion.github.io/assets/downloads/gForce100_manual_v1.1-eng.pdf) and gesture strictly.

> How to connect gForce with gForceJoint wirelessly?

1. Turn on gForce armband, the green led should flash slowly
1. Make sure gForceJoint is powered on
1. Put gForce armband close to gForceJoint such as within 10 cm of distance.
1. gForce armband will automatically connect to gForceJoint. The green led should   flash much faster.
1. If not, make sure gForceJoint is not connected to other gForce armband. Only one armband is allowed. And, make sure, power is on.

**Note**:
One should make sure gForceJoint works with ArduinoMEGA before continuing. Possible mistakes are:

* Wiring mistakes between gForceJoint and ArduinoMEAG
* gForce doesn’t connect with gForceJoint because distance. When connecting, gForce armband and gForceJoint HAVE to be within a short distance as close as possible such as 10 cm.
* User doesn’t follow armband wearing and gestures.
