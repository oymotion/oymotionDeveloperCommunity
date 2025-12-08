
# gForce SDK 手册

***

## 获取数据的函数

|SDK 类型|方位数据|姿态数据|设备状态|Other Data\*|Data Config Function|
|:-|:-|:-|:-|:-|:-|
|gForceCXX|onOrientationData(...)\*\*|onGestureData(...)\*\*|onDeviceStatusChanged(...)\*\*|onExtendedDeviceData(...)\*\*|DeviceSetting::setDataNotifSwitch(...)|
|gForceCSharp|onOrientationData(...)\*\*|onGestureData(...)\*\*|onDeviceStatusChanged(...)\*\*|onExtendedDeviceData(...)\*\*|Device::setDataSwitch(...)|
|gForcePython|Callback of GF.startDataNotification(...)|Callback of GF.startDataNotification(...)|Callback of GF.startDataNotification(...)|Callback of GF.startDataNotification(...)|GF.setDataNotifSwitch(...)|
|gForceArduino|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)\*\*\*|NA|
|gForceEmbedded|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)|GForceAdapter::GetGForceData(...)\*\*\*|NA|

**注意**:

\* : 包含10种数据类型

\*\* : 在HubListener的子类中

\*\*\* : 仅支持EMG数据

***

## 回调中的数据格式

当所需的数据通知到来时，将调用回调函数（例如：在 HubListener 的子类中的 onExtendedDeviceData(...) 方法，或 GF.startDataNotification(...) 的用户回调函数）

数据格式:

|通知数据类型|数据包长度|首字节数值|数据内容\*|注释|
|:-|:-|:-|:-|:-|
|Accelerator|13|0x01 (NTF_ACC_DATA)|Accelerator_X(4 Byte long), Accelerator_Y, Accelerator_Z|x、y、z轴的加速度值，采用q15格式。将其除以65536.0f可获得实际浮点数值|
|Gyroscope|13|0x02 (NTF_GYRO_DATA)|Gyroscope_X(4 Byte long), Gyroscope_Y, Gyroscope_Z|x、y、z轴的陀螺仪数据，采用q15格式。将其除以65536.0f可获得实际浮点数值|
|Magnetometer|13|0x03 (NTF_MAG_DATA)|Gyroscope_X(4 Byte long), Compass_Y, Compass_Z|x、y、z轴的磁力计数据，采用q15格式。将其除以65536.0f可获得实际浮点数值|
|Euler Angle|13|0x04 (NTF_EULER_DATA)|Pitch(4 Byte float), Roll, Yaw|欧拉角数据单位为度。俯仰角（Pitch）和偏航角（Yaw）范围均为[-180, 180]，翻滚角（Roll）范围为[-90, 90]|
|Quaternion|17|0x05 (NTF_QUAT_FLOAT_DATA)|Quaternion_W(4 Byte float), Quaternion_X, Quaternion_Y, Quaternion_Z|四元数，是简单的超复数|
|Rotation Matrix|37|0x06 (NTF_ROTA_DATA)|Rot[0][0], Rot[0][1], Rot[0][2], Rot[1][0],...|这是一个3x3旋转矩阵，数据类型为long型。前3个4字节整数表示矩阵的第一行，后续依次为第二行和第三行|
|Gesture|3|0x07 (NTF_EMG_GEST_DATA)|Gesture identify(1 Byte uint), Probability(1 Byte uint)|概率值的范围在[0, 100]之间|
|Raw EMG|129|0x08 (NTF_EMG_ADC_DATA)|CH0,CH1...CH7, CH0,CH1...CH7, ...|数据包长度取决于EMG（肌电图）的配置，默认长度为129字节。当分辨率设置为8时，每个通道的数据由1字节表示；若分辨率设为12，则每个通道的数据需要2字节表示|
|Mouse|NA|0x09 (NTF_HID_MOUSE)|NA|当前不支持此功能|
|Joystick|NA|0x0A (NTF_HID_JOYSTICK)|NA|当前不支持此功能|
|Device Status|2|0x0B (NTF_DEV_STATUS)|bit0 is for Recenter status, bit1 is for USB insert, bit2 is for USB unplug, bit3 is for motionless status; bit4 - bit7 is reserved|使用1字节表示新设备状态|
|Log Message|>= 1|0x0C (NTF_LOG_DATA)|log message string||

\* : 从数据包的第二个字节开始

***

## gForce数据获取示例

EMG原始数据获取示例

*注意：* 此处仅包含数据相关函数，完整示例请参考[SDK list](./SDKList.md)中的代码.

### C++

1\. 实现 `HubListener` 接口

```c++
  class HubListenerImpl : public HubListener{...}
```

2\. 配置 EMG 数据

调用 `DeviceSetting::setEMGRawDataConfig(...)` 来配置EMG数据. 第一个参数是采样率(单位:hz), 第二个参数是通道掩码, 第三个参数是数据包长度, 第四个参数是ADC分辨率, 第五个参数是回调函数.

3\. 打开数据通知

调用 `DeviceSetting::setDataNotifySwitch(...)` 来打开EMG原始数据通知. 将第一个参数设置为DeviceSetting::DNF_EMG_RAW

4\. 提取EMG数据等

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

1\. 继承 `HubListener` 类并实现虚函数.

```c++
  class Listener : HubListener{...}
```

2\. 调用 Device::setEmgConfig(...)来配置EMG数据

```CSharp
connectedDevice.setEmgConfig(650/*sampleRateHz*/, 0x00FF/*interestedChannels*/, 128/*packageDataLength*/, 8/*adcResolution*/, (Device dev, uint resp) =>
{
  // Process the result
});
```

3\. 调用 Device::setDataSwitch(...)打开EMG原始数据通知

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

3\. 打印EMG原始数据

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

**注意**: 配置数据类型及启动/停止数据通知时，应关闭数据传输
