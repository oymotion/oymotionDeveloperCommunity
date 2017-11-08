---
layout: default
title:  "Welcome to the OYMotion Community!"
---

---
## gForce Armband
gForce 100 Armband is a smart wearable [Human Interface Device][HID] for
[gesture recognition][GestureRecognition]. It recognizes gestures according
to the sEMG signals of human forearms, and as well as calculates orientation
data in quaternions or [Euler Angles][EulerAngles] from its built-in 6-axis
[IMU][IMU] and tri-axis [magnetometer][magnetometer].

### Documents
* [gForce 100 Manual][gForce100Manual] &
  [gForce 100 User Guide][gForce100UserGuide]

  The User Guide provides more detailed information than the Manual.

* [gForce 100 Embedded Suite User Guide][gForce100EmbeddedUserGuide]

  Provides guide of using gForce 100 in embedded devices such as robots and
  prosthetics.

* [gForce Data Protocol][gForceDataProtocol]

  The specification of gForce Data Protocol defines the details of gForce
  interacting with host computers of PC, AR and VR.

* [gForce EMG Raw Data][gForceEMGRawData]

  Provides more information about using EMG raw data.

### Open Source Software
* [gForce SDK for Arduino][gForceSDKArduino]

  The open source library with example code to illustrate how to connnect
  gForce to Arduino-alike devices.

* [gForce Data Protocol Sample][gForceDataProtocolSample]

  An open source simple example developed for Android to illustrate
  [gForce Data Protocol](doc/gForceDataProtocol).

* [gForce SDK][gForceSDK]

  The SDK for Windows and Android with Unity support.   
  Internal testing, coming soon......

* [gForceApp][gForceApp]

  The **hub** application for other applications to interact with
  gForce. It also provides utilities for users setting, firmware upgrading and
  diagnosing gForce. Released APK is open for downloading.
  Internal testing, coming soon......

### Downloads
* [gForceApp for Android  gForceApp_v2.3.4-20171009.apk][gForceAPK]

    Pre-built releases of gForceApp for Android.

* [sEMG Raw Data Capture Utility][RawDataCaptureFor100]

    Only for gForce 100 with support for raw data capturing.

* [sEMG Raw Data Capture SDK][RawDataCaptureSDKFor100]

    Only for gForce 100 with support for raw data capturing.
	
### Examples
* [gForce Examples][gForceExample]

  The collection of gForce Armband application examples, like controlling a mechanical hand.

---
## gForce Neuron
### Documents
* [gForce Neuron User Guide](doc/gForceNeuronUserGuide)

### Open Source Software
* [sEMG Filters Library][EMGFilters]

  Provides some basic filter functions for sEMG digital signals.


[HID]: https://en.wikipedia.org/wiki/Human_interface_device
[GestureRecognition]: https://en.wikipedia.org/wiki/Gesture_recognition
[EulerAngles]: https://en.wikipedia.org/wiki/Euler_angles
[IMU]: https://en.wikipedia.org/wiki/Inertial_measurement_unit
[magnetometer]:https://en.wikipedia.org/wiki/Magnetometer
[gForceSDKArduino]: https://github.com/oymotion/gForceSDKArduino
[gForceDataProtocolSample]: https://github.com/oymotion/gForceDataProtocolSample
[EMGFilters]: https://github.com/oymotion/EMGFilters
[gForceSDK]: https://github.com/oymotion/gForceSDK
[gForceApp]: https://github.com/oymotion/gForceApp
[gForceAppForAndroid]: https://github.com/oymotion/gForceApp/releases
[gForceExample]: https://github.com/oymotion/gForceExample
[gForce100UserGuide]: ./gForce100/gForce100UserGuide.md
[gForce100EmbeddedUserGuide]: ./gForceEmbeddedSuit/gForce100EmbeddedSuiteUserGuide.md
[gForceEMGRawData]: ./gForceEMGRawData/gForceEMGRawData.md
[gForceAPK]: ./assets/downloads/gForceApp_v2.3.4-20171009.apk
[RawDataCaptureFor100]: ./assets/downloads/RawDataCapture.zip
[RawDataCaptureSDKFor100]:./assets/downloads/RawDataCaptureSDK.zip
[gForce100Manual]: ./assets/downloads/gForce100_manual_v1.1-eng.pdf
[gForceDataProtocol]: ./gForceDataProtocol/gForceDataProtocol.md