
# gForce SDK Manual

***

## Functions to Get Data

|SDK Type|Orientation Data|Gesture Data|Device Status|Other Data\*|Data Config Function|
|:-|:-|:-|:-|:-|:-|
|gForceCXX|onOrientationData(...)\*\*|onGestureData(...)\*\*|onDeviceStatusChanged(...)\*\*|onExtendedDeviceData(...)\*\*|DeviceSetting::setDataNotifSwitch(...)|
|gForceCSharp|onOrientationData(...)\*\*|onGestureData(...)\*\*|onDeviceStatusChanged(...)\*\*|onExtendedDeviceData(...)\*\*|Device::setDataSwitch(...)|
|gForcePython|Callback of GF.startDataNotification(...)|Callback of GF.startDataNotification(...)|Callback of GF.startDataNotification(...)|Callback of GF.startDataNotification(...)|GF.setDataNotifSwitch(...)|
|gForceArduino|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)\*\*\*|NA|
|gForceEmbedded|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)\*\*\*|NA|

**Note**:

\* : Includes 10 data types

\*\* : In subclass of HubListener

\*\*\* : Only EMG data supported.

***

## Data Format in Callback

Callback will be invoked (e.g., `onExtendedDeviceData(...)` in subclass of HubListener or user callback of `GF.startDataNotification(...)`) when desired data notification comes.

Data format:

|Notification Data Type|Data Packet Length|First Byte Value|Data Content\*|Comment|
|:-|:-|:-|:-|:-|
|Accelerator|13|0x01 (NTF_ACC_DATA)|Accelerator_X(4 Byte long), Accelerator_Y, Accelerator_Z|Accelerate speed of axis x,y and z in q15 format. Divide it by 65536.0f to get real float value.|
|Gyroscope|13|0x02 (NTF_GYRO_DATA)|Gyroscope_X(4 Byte long), Gyroscope_Y, Gyroscope_Z|Gyro of axis x,y and z in q15 format. Divide it by 65536.0f to get real float value.|
|Magnetometer|13|0x03 (NTF_MAG_DATA)|Gyroscope_X(4 Byte long), Compass_Y, Compass_Z|Magneto data of axis x,y and z in q15 format. Divide it by 65536.0f to get real float value.|
|Euler Angle|13|0x04 (NTF_EULER_DATA)|Pitch(4 Byte float), Roll, Yaw|Euler angle data is in degree. Pitch and Yaw is in the range of [-180, 180], Roll is in the range of [-90, 90]|
|Quaternion|17|0x05 (NTF_QUAT_FLOAT_DATA)|Quaternion_W(4 Byte float), Quaternion_X, Quaternion_Y, Quaternion_Z||
|Rotation Matrix|37|0x06 (NTF_ROTA_DATA)|Rot[0][0], Rot[0][1], Rot[0][2], Rot[1][0],...|3*3 Rotation matrix of data type long, leading 3 4-bytes integer represent the first row of matrix and so on|
|Gesture|3|0x07 (NTF_EMG_GEST_DATA)|Gesture identify(1 Byte uint), Probability(1 Byte uint)|Possibility is in the range of [0, 100]|
|Raw EMG|129|0x08 (NTF_EMG_ADC_DATA)|CH0,CH1...CH7, CH0,CH1...CH7, ...|Packet length depends on config of EMG, default 129. If resolution set to 8, 1 byte represents data of 1 channel. 2 bytes for 1 channel incase of resolution=12.|
|Mouse|NA|0x09 (NTF_HID_MOUSE)|NA|Not currently supported|
|Joystick|NA|0x0A (NTF_HID_JOYSTICK)|NA|Not currently supported|
|Device Status|2|0x0B (NTF_DEV_STATUS)|bit0 is for Recenter status, bit1 is for USB insert, bit2 is for USB unplug, bit3 is for motionless status; bit4 - bit7 is reserved|1 Byte for new device status|
|Log Message|>= 1|0x0C (NTF_LOG_DATA)|log message string||

\* : Starts from second byte of data packet.

***

## Examples For Getting Data from gForce

Get EMG raw data examples.

*Note:* Only data related functions here, for complete example, refer to code in [SDK list](./SDKList.md) please.

### C++

1\. Implement `HubListener` interface

```c++
  class HubListenerImpl : public HubListener{...}
```

2\. Config EMG Data

Call `DeviceSetting::setEMGRawDataConfig(...)` to configure Emg. First parameter is sample Rate in Hz, second parameter is channel Mask, third parameter is package data length, fourth parameter is Adc resolution, Fifth parameter is callback function.

3\. Open Data Notification

Call `DeviceSetting::setDataNotifySwitch(...)` to open EMG raw. Set first parameter as DeviceSetting::DNF_EMG_RAW

4\. Extract the data of EMG, etc.

```C++
void HubListenerImpl::onExtendedDeviceData(SPDEVICE device, DeviceDataType dataType, gfsPtr<const vector<GF_UINT8>> data) override
{
  auto ptr = data->data();

  switch (dataType) {
  case DeviceDataType::DDT_EMGRAW:
      for (size_t i = 0; i < data->size(); i++)
      {
        //for 8bpp mode
        printf("Emg data [%d] = %u\n", i, *(reinterpret_cast<const uint8_t*>(ptr++)));

        //for 12bpp mode
        //   printf("Emg data [%d] = %u\n", i, *(reinterpret_cast<const uint16_t*>(ptr)));
        //   ptr += 2;
      }

    break;

  case DeviceDataType::DDT_GYROSCOPE:
      //... extract gyroscope data form 'data'
    break;

  default:
    break;
  }
}
```

***

### Python

```python
DATA_LEN = 128

def ondata(data):
    if data[0] == NotifDataType['NTF_EMG_ADC_DATA'] and len(data) == DATA_LEN + 1:
            # Data for EMG CH0~CHn repeatedly.
            # Resolution set in setEmgRawDataConfig:
            #   8: one byte for one channel
            #   12: two bytes in LSB for one channel.
            # eg. 8bpp mode, data[1] = channel[0], data[2] = channel[1], ... data[8] = channel[7]
            #                data[9] = channel[0] and so on
            # eg. 12bpp mode, {data[2], data[1]} = channel[0], {data[4], data[3]} = channel[1] and so on
            for i in range(1, DATA_LEN):
                print(data[i])

def set_cmd_cb(resp):
    print('Command result: {}'.format(resp))

GF = GForceProfile()
GF.setEmgRawDataConfig(sampRate = 650, channelMask = 0xFF, dataLen = DATA_LEN, resolution = 8, cb = set_cmd_cb, timeout = 1000)
GF.setDataNotifSwitch(DataNotifFlags['DNF_EMG_RAW'], set_cmd_cb, timeout = 1000)
GF.startDataNotification(ondata)

button = input()

if len(button) != 0:
    GF.stopDataNotification()
    GF.setDataNotifSwitch(DataNotifFlags['DNF_OFF'], set_cmd_cb, timeout = 1000)
```

***

### CSharp

1\. Inherit `HubListener` class and implement virtual functions.

```c++
  class Listener : HubListener{...}
```

2\. Call Device::setEmgConfig(...) configure EMG data

```CSharp
connectedDevice.setEmgConfig(650/*sampleRateHz*/, 0x00FF/*interestedChannels*/, 128/*packageDataLength*/, 8/*adcResolution*/, (Device dev, uint resp) =>
{
  // Process the result
});
```

3\. Call Device::setDataSwitch(...) open EMG raw

```CSharp
connectedDevice.enableDataNotification(0); // Stop notification temporary

connectedDevice.setDataSwitch((uint)DataNotifFlags.DNF_EMG_RAW/*and other data flags you want*/, (Device dev, uint resp) =>
{
    System.Console.WriteLine("setDataSwitch, response : {0}", (RetCode)resp);

    if ((RetCode)resp == RetCode.GF_SUCCESS)
    {
        dev.enableDataNotification(1);  // Enable notification
    }
});
```

3\. print the data of EMG raw

```CSharp
class Listener : HubListener
{
  public override void onExtendedDeviceData(Device device, Device.DataType type, byte[] data)
  {
    if (type == Device.DataType.Emgraw)
    {
        System.Console.Write("Emg data len: {0}, data:" , data.Length);

        var sb = new StringBuilder("{");

        foreach (var b in data)
        {
            sb.Append(b + ",");
        }

        sb.Remove(sb.Length - 1, 1);
        sb.Append("}");

        System.Console.WriteLine(sb.ToString());
    }
  }
}
```

**Note**: Data transfers should be off when configuring data types and starting/stopping data notification.
