# Python SDK

## 1.Introduction

This SDK provides convenient Python interfaces for the secondary development of the Aoyi Smart Hand. It allows developers to manage device connection, data acquisition, and gesture control, thereby accelerating the development of applications utilizing the Smart Hand.

## 2.Supported Operating Systems and Software Versions

- ### Operating System

Windows (64-bit & 32-bit): Support for both 64-bit and 32-bit versions on the Windows operating system, facilitating development for Windows users.
Linux (x86 & ARM): Support for both x86 and ARM architectures on the Linux operating system, meeting the requirements of diverse hardware environments.

- ### Software Version

Python 3.12 and above: This development kit is targeted for Python 3.12 and later，ensuring compatibility with the latest Python versions.

## 3.Installation and Usage  

- ### Installation

Download the SDK Locally：

- Method 1: [Click this link](../../../assets/downloads/ROHand/ohand_serial_sdk_python-main.zip) to download  

- Method 2: Visit [ohand_serial_sdk_python](https://github.com/oymotion/ohand_serial_sdk_python){: target="_blank"} Github page to get the latest Python SDK  

- Method 3: Obtain via clone:  

    ```Bash
    git clone https://github.com/oymotion/ohand_serial_sdk_python
    ```

- ### Usage  

Upon successful installation, users can import the SDK into their Python scripts and leverage the API for Smart Hand development. The following code snippet demonstrates the primary code for connecting to the Smart Hand (available in the simple_control.py file):  

```python
def main():
    interface_instance = None
    ohand_instance = None
    if PORT_TYPE == PORT_UART:
        interface_instance = Serial_Init(port_name=find_comport("CH340") or find_comport("Serial"), baudrate=115200)
    else:
        interface_instance = CAN_Init(port_name="1", baudrate=1000000)

    if interface_instance is None:
        print("Port init failed\n")
        return

    ohand_instance = OHandSerialAPI(interface_instance, HAND_PROTOCOL_UART, ADDRESS_MASTER,
                                           send_data_impl, recv_data_impl)

    ohand_instance.HAND_SetTimerFunction(get_milli_seconds_impl, delay_milli_seconds_impl)
    ohand_instance.HAND_SetCommandTimeOut(255)
    print(ohand_instance.get_private_data(), "\n")
```

The output is shown below:  

![初始化.png](../imgs/初始化.png)

## 4.API Reference

### <span style="background-color: #e7f4ffff;color: red;"> _init_()</span>  

- Method Signature：  

```python
def __init__(self, private_data, protocol, address_master, send_data_impl, recv_data_impl=None):  
```

- Parameters:  

  <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>self.address_master = address_master</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>self.protocol = protocol</code></td>
        <td>Communication Protocol</td>
        </tr>
        <tr>
        <td><code>self.private_data = private_data</code></td>
        <td> Internal private data storage for the class.</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>self.recv_data_impl = recv_data_impl</code></td>
        <td>Receiver Function</td>
        </tr>
        <tr>
        <td><code>self.send_data_impl = send_data_impl</code></td>
        <td>Send Function</td>
        </tr>
    </tbody>
  </table>  

- Return Value：
  Status: None on success  
  Failure: Return the corresponding error code

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SendCmd()</span>  

- Method Signature：

```python
def HAND_SendCmd(self, addr, cmd, data, nb_data):
```

- Parameters：  

    <table>
        <thead>
            <tr style="background-color: #e6f7ff;">
            <th>Parameter</th>
            <th>Description</th>
            </tr>
        </thead>
        <tbody>
            <tr>
            <td><code>cmd</code></td>
            <td>Command ID</td>
            </tr>
            <tr style="background-color: #e6f7ff;">
            <td><code>data</code></td>
            <td>Command Data</td>
            </tr>
            <tr>
            <td><code>nb_data</code></td>
            <td>Data Length</td>
            </tr>
        </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetResponse()</span>  

- Method Signature：  

```python
def HAND_GetResponse(self, addr, cmd, time_out, resp_bytes, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>addr</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>cmd</code></td>
        <td>命Command ID令ID</td>
        </tr>
        <tr>
        <td><code>time_out</code></td>
        <td>Timeout Period</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>resp_bytes</code></td>
        <td>Response Data Buffer</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

### <span style="background-color: #e7f4ffff;color: red;"> HAND_OnData()</span>  

- Method Signature：  

```python
HAND_OnData(data)
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>date</code></td>
        <td>Date</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

### <span style="background-color: #e7f4ffff;color: red;"> HAND_HAND_SetTimerFunctionOnData()</span>  

- Method Signature：  

```python
def HAND_SetTimerFunction(self, get_milli_seconds_impl, delay_milli_seconds_impl):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>get_milli_seconds_impl</code></td>
        <td>Gets the current time</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>delay_milli_seconds_impl</code></td>
        <td>Delay Function</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetProtocolVersion()</span>  

- Method Signature：  

```python
def HAND_GetProtocolVersion(self, hand_id, major, minor, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>major</code></td>
        <td>Outputs the major version numberParameter</td>
        </tr>
        <tr>
        <td><code>minor</code></td>
        <td>次版本号输出Parameter</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
major, minor = [0], [0]
err, major_get, minor_get = serial_api_instance.HAND_GetProtocolVersion(hand_id, major, minor, [])
assert err == HAND_RESP_SUCCESS, f"获取协议版本失败: {err}"
logger.info(f"成功获取协议版本: V{major_get}.{minor_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFirmwareVersion()</span>  

- Method Signature：  

```python
def HAND_GetFirmwareVersion(self, hand_id, major, minor, revision, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>major</code></td>
        <td>Outputs the major version number parameter</td>
        </tr>
        <tr>
        <td><code>minor</code></td>
        <td>Outputs the minor version number parameter</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>revision</code></td>
        <td>Outputs the revision number parameter</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
major, minor, revision = [0], [0], [0]
err, major_get, minor_get, revision_get = serial_api_instance.HAND_GetFirmwareVersion(hand_id, major, minor, revision, [])
assert err == HAND_RESP_SUCCESS, f"获取固件版本失败: {err}"
logger.info(f"成功获取固件版本: V{major_get}.{minor_get}.{revision_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetHardwareVersion()</span>  

- Method Signature：  

```python
def HAND_GetHardwareVersion(hand_id, hw_type, hw_ver, boot_version, remote_err)
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>功能</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>hw_type</code></td>
        <td>Hardware Type Output Parameter</td>
        </tr>
        <tr>
        <td><code>hw_ver</code></td>
        <td>Hardware Version Output Parameter</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>boot_version</code></td>
        <td>Bootloader Version Output Parameter</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
hw_type, hw_ver, boot_version = [0], [0], [0]
err, hw_type_get, hw_ver_get, boot_version_get = serial_api_instance.HAND_GetHardwareVersion(hand_id, hw_type, hw_ver, boot_version, [])
assert err == HAND_RESP_SUCCESS, f"获取硬件版本失败: {err}"
logger.info(f"成功获取硬件版本: V{hw_type_get}.{hw_ver_get}.{boot_version_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetCaliData()</span>

- Method Signature：  

```python
def HAND_GetCaliData(self, hand_id, end_pos, start_pos, motor_cnt, thumb_root_pos, thumb_root_pos_cnt, remote_err):
```

- Parameters：  

    <table>
      <thead>
          <tr style="background-color: #e6f7ff;">
          <th>Parameter</th>
          <th>Description</th>
          </tr>
      </thead>
      <tbody>
          <tr>
          <td><code>hand_id</code></td>
          <td>Device Address</td>
          </tr>
          <tr style="background-color: #e6f7ff;">
          <td><code>end_pos</code></td>
          <td>End Position Array</td>
          </tr>
          <tr>
          <td><code>start_pos</code></td>
          <td>Start Position Array</td>
          </tr>
          <tr style="background-color: #e6f7ff;">
          <td><code>motor_cnt</code></td>
          <td>Motor Quantity</td>
          </tr>
          <tr>
          <td><code>thumb_root_pos</code></td>
          <td>Thumb Base Position Array</td>
          </tr>
          <tr style="background-color: #e6f7ff;">
          <td><code>thumb_root_pos_cnt</code></td>
          <td>Thumb Base Position Gear</td>
          </tr>
          <tr>
          <td><code>remote_err</code></td>
          <td>Remote Error Code Storage</td>
          </tr>
      </tbody>
      </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
end_pos = [0] * MAX_MOTOR_CNT
start_pos = [0] * MAX_MOTOR_CNT
motor_cnt = [MAX_MOTOR_CNT]
thumb_root_pos = [0] * MAX_THUMB_ROOT_POS
thumb_root_pos_cnt = [3]  # 初始请求3个拇指根位置Date
err, end_pos_get, start_pos_get, thumb_root_pos_get = serial_api_instance.HAND_GetCaliData(hand_id, end_pos, start_pos, motor_cnt, thumb_root_pos, thumb_root_pos_cnt, [])
assert err == HAND_RESP_SUCCESS, f"获取矫正Date失败: {err}"
logger.info(f"成功获取矫正Date, end_pos: {end_pos_get}, start_pos: {start_pos_get}, thumb_root_pos: {thumb_root_pos_get}, ")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerPID()</span>

- Method Signature：

```python
def HAND_GetFingerPID(self, hand_id, finger_id, p, i, d, g, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
        </tr>
        <tr>
        <td><code>p</code></td>
        <td>比例ParameterP</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>i</code></td>
        <td>积分ParameterI</td>
        </tr>
        <tr>
        <td><code>d</code></td>
        <td>微分ParameterD</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>g</code></td>
        <td>重力补偿ParameterG</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
p, i, d, g = [0], [0], [0], [0]
for j in range(MAX_MOTOR_CNT):
  err, p_get, i_get, d_get, g_get = serial_api_instance.HAND_GetFingerPID(hand_id, j, p, i, d, g, None)
  assert err == HAND_RESP_SUCCESS, f"获取pidDate失败: {err}"
  logger.info(f"成功获取手指: {j} pidDate: p: {p_get} i: {i_get} d: {d_get} g: {g_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerCurrentLimit()</span>

- Method Signature：  

```python
def HAND_GetFingerCurrentLimit(self, hand_id, finger_id, current_limit, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
        </tr>
        <tr>
        <td><code>current_limit</code></td>
        <td>电流限制值（单位：  mA或其他硬件相关单位）</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
current_limit = [0]
for i in range(MAX_MOTOR_CNT):
  err, current_limit_get = serial_api_instance.HAND_GetFingerCurrentLimit(hand_id, i, current_limit, None)
  assert err == HAND_RESP_SUCCESS, f"获取电流最大值失败: {err}"
  logger.info(f"成功获取手指: {i} 电流最大值: {current_limit_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerCurrent()</span>

- Method Signature：  

```python
def HAND_GetFingerCurrent(self, hand_id, finger_id, current, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
        </tr>
        <tr>
        <td><code>current</code></td>
        <td>实时电流值</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
current = [0]
for i in range(MAX_MOTOR_CNT):
  err, current_get = serial_api_instance.HAND_GetFingerCurrent(hand_id, i, current, [])
  assert err == HAND_RESP_SUCCESS, f"获取电流最大值失败: {err}"
  logger.info(f"成功获取手指: {i} 电流值: {current_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerForceTarget()</span>

- Method Signature：  

```python
def HAND_GetFingerForceTarget(self, hand_id, finger_id, force_target, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>force_target</code></td>
        <td>Target Force Value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
force_target = [0]
for i in range(MAX_MOTOR_CNT):
  err, force_target_get = serial_api_instance.HAND_GetFingerForceTarget(hand_id, i, force_target, [])
  assert err == HAND_RESP_SUCCESS, f"手指力值目标失败: {err}"
  logger.info(f"成功获取手指: {i} 力值目标: {force_target_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerForce()</span>

- Method Signature：  

```python
def HAND_GetFingerForce(self, hand_id, finger_id, force_entry_cnt, force, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>force_entry_cnt</code></td>
        <td>Number of Actual Force Data Entries</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force</code></td>
        <td>Force Data Array</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
force = [0] * MAX_FORCE_ENTRIES
force_entry_cnt = [0]
for i in range(MAX_MOTOR_CNT):
  err, force_get = serial_api_instance.HAND_GetFingerForce(hand_id, i, force_entry_cnt, force, [])
  assert err == HAND_RESP_SUCCESS, f"手指每点力值失败: {err}"
  logger.info(f"成功获取手指: {i} 力值每点: {force_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GeHAND_GetFingerPosLimittFingerForce()</span>

- Method Signature：  

```python
def HAND_GetFingerPosLimit(self, hand_id, finger_id, low_limit, high_limit, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>low_limit</code></td>
        <td>Lower Position Limit (Minimum Position)</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>high_limit</code></td>
        <td>Upper Position Limit (Maximum Position)</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
low_limit, high_limit = [0], [0]
for i in range(MAX_MOTOR_CNT):
  err, low_limit_get,high_limit_get  = serial_api_instance.HAND_GetFingerPosLimit(hand_id, i, low_limit, high_limit, [])
  assert err == HAND_RESP_SUCCESS, f"获取手指限位值失败: {err}"
  logger.info(f"成功获取手指: {i} 限位值low: {low_limit_get}, 限位值high: {high_limit_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerPosAbs()</span>

- Method Signature：  

```python
def HAND_GetFingerPosAbs(self, hand_id, finger_id, target_pos, current_pos, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>target_pos</code></td>
        <td>Target Absolute Position (Raw Encoder Value)</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_pos</code></td>
        <td>Current Absolute Position (Raw Encoder Value)</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
target_pos, current_pos = [0], [0]
for i in range(MAX_MOTOR_CNT):
  err, target_pos_get, current_pos_get = serial_api_instance.HAND_GetFingerPosAbs(hand_id, i, target_pos, current_pos, [])
  assert err == HAND_RESP_SUCCESS, f"获取手指绝对位置失败: {err}"
  logger.info(f"成功获取手指: {i} 目标绝对位置: {target_pos_get}, 当前绝对位置: {current_pos_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerPos()</span>

- Method Signature：  

```python
def HAND_GetFingerPos(self, hand_id, finger_id, target_pos, current_pos, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>target_pos</code></td>
        <td>Target Logical Position (Calibrated Mapping Value)）</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_pos</code></td>
        <td>Current Logical Position (Calibrated Mapping Value)</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
target_pos, current_pos = [0], [0]
for i in range(MAX_MOTOR_CNT):
  err, target_pos_get, current_pos_get = serial_api_instance.HAND_GetFingerPos(hand_id, i, target_pos, current_pos, [])
  assert err == HAND_RESP_SUCCESS, f"获取手指位置失败: {err}"
  logger.info(f"成功获取手指: {i} 目标位置: {target_pos_get}, 当前位置: {current_pos_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerAngle()</span>

- Method Signature：  

```python
def HAND_GetFingerAngle(self, hand_id, finger_id, target_angle, current_angle, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>target_angle</code></td>
        <td>Target Angle Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_angle</code></td>
        <td>Current Angle Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
target_angle, current_angle = [0], [0]
for i in range(MAX_MOTOR_CNT):
  err, target_angle_get, current_angle_get = serial_api_instance.HAND_GetFingerAngle(hand_id, i, target_angle, current_angle, [])
  assert err == HAND_RESP_SUCCESS, f"获取手指角度失败: {err}"
  logger.info(f"成功获取手指: {i} 目标角度: {target_angle_get}, 当前角度: {current_angle_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetThumbRootPos()</span>

- Method Signature：  

```python
def HAND_GetThumbRootPos(self, hand_id, raw_encoder, pos, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>raw_encoder</code></td>
        <td>Raw Encoder Value Output Parameter</td>
      </tr>
      <tr>
        <td><code>pos</code></td>
        <td>Calibrated Position Value Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
raw_encoder, pos = [0], [0]
err, raw_encoder_get, pos_get = serial_api_instance.HAND_GetThumbRootPos(hand_id, raw_encoder, pos, [])
assert err == HAND_RESP_SUCCESS, f"获取大拇指位置失败: {err}"
logger.info(f"成功获取大拇指: 原始值: {raw_encoder_get}, 位置: {pos_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerPosAbsAll()</span>

- Method Signature：  

```python
def HAND_GetFingerPosAbsAll(self, hand_id, target_pos, current_pos, motor_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_pos</code></td>
        <td>目Absolute Position Array Output Parameter (Raw Encoder Values)</td>
      </tr>
      <tr>
        <td><code>current_pos</code></td>
        <td>Current Absolute Position Array Output Parameter (Raw Encoder Values)</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Input/Output Parameter: Motor Count</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
target_pos, current_pos = [0] * MAX_MOTOR_CNT, [0] * MAX_MOTOR_CNT
motor_cnt = [MAX_MOTOR_CNT]
err, target_pos, current_pos = serial_api_instance.HAND_GetFingerPosAbsAll(hand_id, target_pos, current_pos, motor_cnt, [])
assert err == HAND_RESP_SUCCESS, f"获取手指全部绝对位置失败: {err}"
logger.info(f"成功获取全部绝对位置: 当前位置: {current_pos}, 目标位置:{target_pos}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerAngleAll()</span>

- Method Signature：  

```python
def HAND_GetFingerAngleAll(self, hand_id, target_angle, current_angle, motor_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_angle</code></td>
        <td>Target Angle Array Output Parameter</td>
      </tr>
      <tr>
        <td><code>current_angle</code></td>
        <td>Current Angle Array Output Paramete</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Joint Count Parameter (Input/Output)</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
target_angle, current_angle = [0] * MAX_MOTOR_CNT, [0] * MAX_MOTOR_CNT
motor_cnt = [MAX_MOTOR_CNT]
err, target_angle, current_angle = serial_api_instance.HAND_GetFingerAngleAll(hand_id, target_angle, current_angle, motor_cnt, [])
assert err == HAND_RESP_SUCCESS, f"获取手指全部角度失败: {err}"
logger.info(f"成功获取全部角度: 当前角度: {target_angle}, 目标角度:{current_angle}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerStopParams()</span>

- Method Signature：  

```python
def HAND_GetFingerStopParams(self, hand_id, finger_id, speed, stop_current, stop_after_period, retry_interval, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Stop Speed Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>stop_current</code></td>
        <td>Stop Current Threshold Output Parameter</td>
      </tr>
      <tr>
        <td><code>stop_after_period</code></td>
        <td>Stop Wait Time Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>retry_interval</code></td>
        <td>Retry Interval Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
speed, stop_current, stop_after_period, retry_interval = [0], [0], [0], [0]
for i in range(MAX_MOTOR_CNT):
  err, speed_get, stop_current_get, stop_after_period_get, retry_interval_get = serial_api_instance.HAND_GetFingerStopParams(hand_id, i, speed, stop_current, stop_after_period, retry_interval, [])
  assert err == HAND_RESP_SUCCESS, f"获取手指停止Parameter失败: {err}"
  logger.info(f"成功获取手指停止Parameter: 速度: {speed_get}, 暂停电流:{stop_current_get}, 暂停间隔:{stop_after_period_get}, 重试间隔:{retry_interval_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetFingerForcePID()</span>

- Method Signature：  

```python
def HAND_GetFingerForcePID(self, hand_id, finger_id, p, i, d, g, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>p</code></td>
        <td>Proportional Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>i</code></td>
        <td>Integral Parameter</td>
      </tr>
      <tr>
        <td><code>d</code></td>
        <td>Derivative Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>g</code></td>
        <td>Gravity Compensation Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
p, i, d, g = [0], [0], [0], [0]
for j in range(MAX_MOTOR_CNT - 1):
  err, p_get, i_get, d_get, g_get = serial_api_instance.HAND_GetFingerForcePID(hand_id, j, p, i, d, g, [])
  assert err == HAND_RESP_SUCCESS, f"获取手指力pid失败: {err}"
  logger.info(f"成功获取手指力pid: 手指: {j} p: {p_get}, i:{i_get}, d:{d_get}, g:{g_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetSelfTestLevel()</span>

- Method Signature：  

```python
def HAND_GetSelfTestLevel(self, hand_id, self_test_level, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>self_test_level</code></td>
        <td>Self-Test Level Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

```python
self_test_level = [0]
err, self_test_level_get = serial_api_instance.HAND_GetSelfTestLevel(hand_id, self_test_level, [])
assert err == HAND_RESP_SUCCESS, f"获取自检等级失败: {err}"
logger.info(f"成功自检等级: {self_test_level_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetBeepSwitch()</span>

- Method Signature：  

```python
def HAND_GetBeepSwitch(self, hand_id, beep_switch, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>beep_switch</code></td>
        <td>Buzzer Switch Status Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
beep_switch = [0]
err, beep_switch_get = serial_api_instance.HAND_GetBeepSwitch(hand_id, beep_switch, [])
assert err == HAND_RESP_SUCCESS, f"获取蜂鸣器开关失败: {err}"
logger.info(f"成功获取蜂鸣器开关: {beep_switch_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetButtonPressedCnt()</span>

- Method Signature：  

```python
def HAND_GetButtonPressedCnt(self, hand_id, pressed_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pressed_cnt</code></td>
        <td>Button Press Count Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
button_pressed_cnt = [0]
err, button_pressed_cnt_get = serial_api_instance.HAND_GetButtonPressedCnt(hand_id, button_pressed_cnt, [])
assert err == HAND_RESP_SUCCESS, f"获取手按下的数量: {err}"
logger.info(f"获取手按下的数量: {button_pressed_cnt_get}")
```

- **Note: This feature is only available for the bionic hand. It is not available on the dexterous hand.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetUID()</span>

- Method Signature：  

```python
def HAND_GetUID(self, hand_id, uid_w0, uid_w1, uid_w2, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>uid_w0</code></td>
        <td>UID Part 1 Output Parameter</td>
      </tr>
      <tr>
        <td><code>uid_w1</code></td>
        <td>UID Part 2 Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>uid_w2</code></td>
        <td>UID Part 3 Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
uid_w0, uid_w1, uid_w2 = [0], [0], [0]
err, uid_w0_get, uid_w1_get, uid_w2_get = serial_api_instance.HAND_GetUID(hand_id, uid_w0, uid_w1, uid_w2, [])
assert err == HAND_RESP_SUCCESS, f"获取uid: {err}\n"
logger.info(f"获取uid: uid_w0: {uid_w0_get}, uid_w1: {uid_w1_get}, uid_w2: {uid_w2_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetBatteryVoltage()</span>

- Method Signature：  

```python
def HAND_GetBatteryVoltage(self, hand_id, voltage, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>voltage</code></td>
        <td>Battery Voltage Value Output Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- **Note: This feature is only available for the bionic hand. It is not available on the dexterous hand.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetUsageStat()</span>

- Method Signature：  

```python
def HAND_GetUsageStat(self, hand_id, total_use_time, total_open_times, motor_cnt, remote_err):
```

- Purpose：  

  Retrieves usage statistics, reading the hand's total operating time and the individual power-on count for each motor.  

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>total_use_time</code></td>
        <td>Total Usage Time Output Parameter</td>
      </tr>
      <tr>
        <td><code>total_open_times</code></td>
        <td>Motor Total Power-On Count Array Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Motor Count Input Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- **Note: This feature is only available for the bionic hand. It is not available on the dexterous hand.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_GetManufactureData()</span>

- Method Signature：  

```python
def HAND_GetManufactureData(self, hand_id, sub_model, hw_revision, serial_number, customer_tag, remote_err):
```

- Purpose：  

    Retrieves manufacturing data, reading the hand's model, hardware version, serial number, customer tag, and other manufacturing information.

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>sub_model</code></td>
        <td>Model Output Parameter</td>
      </tr>
      <tr>
        <td><code>hw_revision</code></td>
        <td>Hardware Version Output Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>serial_number</code></td>
        <td>Serial Number Output Parameter</td>
      </tr>
      <tr>
        <td><code>customer_tag</code></td>
        <td>Customer Tag Output Paramet</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
sub_model, hw_revision, serial_number, customer_tag = [0], [0], [0], [0]

err, sub_model_get, hw_revision_get, serial_number_get, customer_tag_get = serial_api_instance.HAND_GetManufactureData(hand_id, sub_model, hw_revision, serial_number, customer_tag, [])

assert err == HAND_RESP_SUCCESS, f"manufacture_data_get: {err}\n"
logger.info(f"sub_model: {sub_model_get}, hw_revision: {hw_revision_get}, serial_number: {serial_number_get}, customer_tag: {customer_tag_get}")
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_Reset()</span>

- Method Signature：  

```python
def HAND_Reset(self, hand_id, mode, remote_err):
```

- Parameters：  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>mode</code></td>
        <td>Reset Mode</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
mode = 0
err = serial_api_instance.HAND_Reset(hand_id, mode, [])
assert err == HAND_RESP_SUCCESS, f"HAND_Reset: {err}\n"
delay_milli_seconds_impl(25000)

```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_PowerOff()</span>

- Method Signature：  

```python
def HAND_PowerOff(self, hand_id, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
err = api.HAND_PowerOff(hand_id, [])
assert err == HAND_RESP_SUCCESS, f"power_off_set: {err}\n"
```

- **Note: This feature is only available for the bionic hand. It is not available on the dexterous hand.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetID()</span>

- Method Signature：  

```python
def HAND_SetID(self, hand_id, new_id, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Current Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>new_id</code></td>
        <td>New Device Address</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value：
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
new_id = 0x03
err = serial_api_instance.HAND_SetID(hand_id, new_id, [])
assert err == HAND_RESP_SUCCESS, f"id_set: {err}\n"
serial_api_instance.HAND_SetID(new_id, hand_id, [])
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_Calibrate()</span>

- Method Signature：  

```python
def HAND_Calibrate(self, hand_id, key, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>key</code></td>
        <td>Calibration Key</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetCaliData()</span>

- Method Signature：  

```python
def HAND_SetCaliData(self, hand_id, end_pos, start_pos, motor_cnt, thumb_root_pos, thumb_root_pos_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>end_pos</code></td>
        <td>End Position Array Input</td>
      </tr>
      <tr>
        <td><code>start_pos</code></td>
        <td>Start Position Array Input</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Motor Count</td>
      </tr>
      <tr>
        <td><code>thumb_root_pos</code></td>
        <td>Thumb Base Position Array Input</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>thumb_root_pos_cnt</code></td>
        <td>Thumb Base Position Array Input</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code
  
- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerPID()</span>

- Method Signature：  

```python
def HAND_SetFingerPID(self, hand_id, finger_id, p, i, d, g, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>p</code></td>
        <td>Proportional Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>i</code></td>
        <td>Integral Parameter</td>
      </tr>
      <tr>
        <td><code>d</code></td>
        <td>Derivative Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>g</code></td>
        <td>Gravity Compensation Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
for j in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(finger_set_delay_time)
  err = serial_api_instance.HAND_SetFingerPID(hand_id, j, pid_gains[j][0], pid_gains[j][1], pid_gains[j][2], pid_gains[j][3], remote_err)
  print(f"remote_err: {remote_err}")
  assert err == HAND_RESP_SUCCESS, f"finger: {j}, finger_pid_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerCurrentLimit()</span>

- Method Signature：  

```python
def HAND_SetFingerCurrentLimit(self, hand_id, finger_id, current_limit, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>current_limit</code></td>
        <td>Current Limit Value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerCurrentLimit()</span>

- Method Signature：  

```python
def HAND_SetFingerCurrentLimit(self, hand_id, finger_id, current_limit, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>pos_limit_low</code></td>
        <td>Position Lower Limit</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos_limit_high</code></td>
        <td>Position Upper Limit</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
current_limit_set = 200
current_limit_get = [0]
for i in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(finger_set_delay_time)
  err = serial_api_instance.HAND_SetFingerCurrentLimit(hand_id, i, current_limit_set, [])
  assert err == HAND_RESP_SUCCESS, f"finger: {i}, finger_current_limit_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_FingerStart()</span>

- Method Signature：  

```python
def HAND_FingerStart(self, hand_id, finger_id, pos_limit_low, pos_limit_high, remote_err):
```

- Purpose：

    This function initiates motion for a specified single finger on the target robotic hand device and configures the positional movement limits.  

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>pos_limit_low</code></td>
        <td>Position Lower Limit</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos_limit_high</code></td>
        <td>Position Upper Limit</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
finger_ids = [1, 2, 4, 6, 8, 10]
for i in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(finger_set_delay_time)
  finger_id = finger_ids[i]
  err = serial_api_instance.HAND_FingerStart(hand_id, finger_id, [])
  assert err == HAND_RESP_SUCCESS, f"finger: {i}, test_finger_start_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_FingerStop()</span>

- Method Signature：  

```python
def HAND_FingerStop(self, hand_id, finger_id_bits, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id_bits</code></td>
        <td>Finger Position Mask</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
finger_ids = [1, 2, 4, 6, 8, 10]
for i in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(finger_set_delay_time)
  finger_id = finger_ids[i]
  err = serial_api_instance.HAND_FingerStop(hand_id, finger_id, [])
  assert err == HAND_RESP_SUCCESS, f"finger: {i}, test_finger_stop_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerPosAbs()</span>

- Method Signature：  

```python
def HAND_SetFingerPosAbs(self, hand_id, finger_id, raw_pos, speed, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>raw_pos</code></td>
        <td>Absolute Position Value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>Motion Velocity</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
pos_abs_set = 13000
speed = 100
target_pos, current_pos = [0], [0]
delay_milli_seconds_impl(set_delay_time)
for i in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(finger_set_delay_time)
  err = serial_api_instance.HAND_SetFingerPosAbs(hand_id, i, pos_abs_set, speed, [])
  assert err == HAND_RESP_SUCCESS, f"finger: {i}, test_finger_pos_abs_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerPos()</span>

- Method Signature：  

```python
def HAND_SetFingerPos(self, hand_id, finger_id, pos, speed, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (range: 0-5)</td>
      </tr>
      <tr>
        <td><code>pos</code></td>
        <td>Target Position Value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>Motion Speed</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
pos_set = 32000
speed = 100
target_pos_get, current_pos_get = [0], [0]
for i in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(finger_set_delay_time)
  err = serial_api_instance.HAND_SetFingerPos(hand_id, i, pos_set, speed, [])
  assert err == HAND_RESP_SUCCESS, f"finger: {i}, test_finger_pos_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerAngle()</span>

- Method Signature：  

```python
def HAND_SetFingerAngle(self, hand_id, finger_id, angle, speed, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (0-5)</td>
      </tr>
      <tr>
        <td><code>angle</code></td>
        <td>Target Position Value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>Motion Speed</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
four_finger_angle_set = 12000
thumb_angle_set = 3600
thumb_root_angle_set = 6000
target_angle, current_angle = [0], [0]
speed = 100
for i in range(MAX_MOTOR_CNT):
  delay_milli_seconds_impl(200)
  if(i >= 1 and i <= 4):
      err = serial_api_instance.HAND_SetFingerAngle(hand_id, i, four_finger_angle_set, speed, [])
  elif (i == 0):
      err = serial_api_instance.HAND_SetFingerAngle(hand_id, i, thumb_angle_set, speed, [])
  else:
      err = serial_api_instance.HAND_SetFingerAngle(hand_id, i, thumb_root_angle_set, speed, [])
  assert err == HAND_RESP_SUCCESS, f"finger: {i}, test_finger_angle_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetThumbRootPos()</span>

- Method Signature：  

```python
def HAND_SetThumbRootPos(self, hand_id, pos, speed, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos</code></td>
        <td>Thumb Base Position Value</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Motion Speed</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
pos_set = 1
pos = [0]
speed = 100
raw_encoder = [0]
err = serial_api_instance.HAND_SetThumbRootPos(hand_id, pos_set, speed, [])
assert err == HAND_RESP_SUCCESS, f"test_thumb_root_pos_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerPosAbsAll()</span>

- Method Signature：  

```python
def HAND_SetFingerPosAbsAll(self, hand_id, raw_pos, speed, motor_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>raw_pos</code></td>
        <td>Position Value Array</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Velocity Value Array</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Motor Quantity</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
raw_pos_abs = [13000, 13000, 13000, 13000, 13000, 5000]
raw_speed = [100,100, 100, 100, 100, 100]
motor_cnt = MAX_MOTOR_CNT
raw_target_pos_abs, raw_current_pos_abs = [0] * MAX_MOTOR_CNT, [0] * MAX_MOTOR_CNT

err = serial_api_instance.HAND_SetFingerPosAbsAll(hand_id, raw_pos_abs, raw_speed, motor_cnt, [])
assert err == HAND_RESP_SUCCESS, f"test_finger_pos_abs_all_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerPosAll()</span>

- Method Signature：  

```python
def HAND_SetFingerPosAll(self, hand_id, pos, speed, motor_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos</code></td>
        <td>Position Value Array</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Velocity Value Array</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Motor Quantity</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
raw_pos = [18000, 33000, 33000, 33000, 33000, 38000]
raw_speed = [100, 100, 100, 100, 100, 100]
motor_cnt = MAX_MOTOR_CNT
raw_target_pos, raw_current_pos = [0] * MAX_MOTOR_CNT, [0] * MAX_MOTOR_CNT

err = serial_api_instance.HAND_SetFingerPosAll(hand_id, raw_pos, raw_speed, motor_cnt, [])
assert err == HAND_RESP_SUCCESS, f"test_finger_pos_all_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerAngleAll()</span>

- Method Signature：  

```python
def HAND_SetFingerAngleAll(self, hand_id, angle, speed, motor_cnt, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>angle</code></td>
        <td>Angle Value Array</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Velocity Value Array</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>motor_cnt</code></td>
        <td>Motor Quantity</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
raw_angle = [2000,12000,12000,12000,12000,5000]
raw_speed = [100, 100, 100, 100, 100, 100]
motor_cnt = MAX_MOTOR_CNT
raw_target_angle, raw_current_angle = [0] * MAX_MOTOR_CNT, [0] * MAX_MOTOR_CNT

err = serial_api_instance.HAND_SetFingerAngleAll(hand_id, raw_angle, raw_speed, motor_cnt, [])
assert err == HAND_RESP_SUCCESS, f"test_finger_angle_all_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerStopParams()</span>

- Method Signature：  

```python
def HAND_SetFingerStopParams(self, hand_id, finger_id, speed, stop_current, stop_after_period, retry_interval, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (0-5)</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Motion Speed</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>stop_current</code></td>
        <td>Stop Current Threshold</td>
      </tr>
      <tr>
        <td><code>stop_after_period</code></td>
        <td>Stop Detection Time Period</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>retry_interval</code></td>
        <td>Retry Interval Time</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
speed = 16
stop_current = 200
stop_after_period = 300
retry_interval = 500
speed_get, stop_current_get, stop_after_period_get, retry_interval_get = [0], [0], [0], [0]

for i in range(MAX_MOTOR_CNT):
  err = serial_api_instance.HAND_SetFingerStopParams(hand_id, i, speed, stop_current, stop_after_period, retry_interval, [])
  assert err == HAND_RESP_SUCCESS, f"test_finger_stop_params_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetFingerForcePID()</span>

- Method Signature：  

```python
def HAND_SetFingerForcePID(self, hand_id, finger_id, p, i, d, g, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>finger_id</code></td>
        <td>Finger ID (0-5)</td>
      </tr>
      <tr>
        <td><code>p</code></td>
        <td>Proportional Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>i</code></td>
        <td>Integral Parameter</td>
      </tr>
      <tr>
        <td><code>d</code></td>
        <td>Derivative Parameter</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>g</code></td>
        <td>Gravity Compensation Parameter</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
p, i, d, g = [0], [0], [0], [0]

for j in range(MAX_MOTOR_CNT - 1):
  delay_milli_seconds_impl(finger_set_delay_time)
  err = serial_api_instance.HAND_SetFingerForcePID(hand_id, j, force_pid[j][0], force_pid[j][1], force_pid[j][2], force_pid[j][3], [])
  assert err == HAND_RESP_SUCCESS, f"test_finger_force_pid_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_ResetForce()</span>

- Method Signature：  

```python
def HAND_ResetForce(self, hand_id, remote_err):
```

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
err = serial_api_instance.HAND_ResetForce(hand_id, [])
assert err == HAND_RESP_SUCCESS, f"test_force_reset: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_ResetForce()</span>

- Method Signature：  

```python
def HAND_ResetForce(self, hand_id, remote_err):
```

- Purpose：

  This function is used to send custom commands to the robotic hand device, supporting bidirectional data transmission. It provides a generic and extensible interface that enables users to transmit specific data and receive device responses, facilitating the implementation of non-standard or extended functionalities.  

- Parameters：  

  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data</code></td>
        <td>Data Buffer</td>
      </tr>
      <tr>
        <td><code>send_data_size</code></td>
        <td>Sent Data Size</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>recv_data_size</code></td>
        <td>Received Data Size</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
err = serial_api_instance.HAND_ResetForce(hand_id, [])
assert err == HAND_RESP_SUCCESS, f"test_force_reset: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetSelfTestLevel()</span>

- Method Signature：  

```python
def HAND_SetSelfTestLevel(self, hand_id, self_test_level, remote_err):
```

- Parameters：  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>self_test_level</code></td>
        <td>Self-Test Level</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
self_test_level_set = 2
self_test_level = [0]

err = serial_api_instance.HAND_SetSelfTestLevel(hand_id, self_test_level_set, [])
assert err == HAND_RESP_SUCCESS, f"test_self_test_level: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetBeepSwitch()</span>

- Method Signature：  

```
    def HAND_SetBeepSwitch(self, hand_id, beep_on, remote_err):
```

- Parameters：  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>beep_on</code></td>
        <td>Buzzer Switch Status</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
beep_switch_set = 1
beep_switch = [0]

err = serial_api_instance.HAND_SetBeepSwitch(hand_id, beep_switch_set, [])
assert err == HAND_RESP_SUCCESS, f"test_beep_switch_set: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_Beep()</span>

- Method Signature：  

```python
def HAND_Beep(self, hand_id, duration, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>duration</code></td>
        <td>Buzzer Duration</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
duration = 200
err = serial_api_instance.HAND_Beep(hand_id, duration, [])
assert err == HAND_RESP_SUCCESS, f"test_beep: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetButtonPressedCnt()</span>

- Method Signature：  

```python
def HAND_SetButtonPressedCnt(self, hand_id, pressed_cnt, remote_err):
```

- Purpose：  

  This function configures the button press counting mechanism of the robotic hand, allowing the user to set a trigger threshold for the number of button presses or reset the current count. It is commonly used to define how many button presses are required to activate a specific function or to reset the counter to its initial state.  

- Parameters：

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>pressed_cnt</code></td>
        <td>按钮按下计数</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**

### <span style="background-color: #e7f4ffff;color: red;"> HAND_StartInit()</span>

- Method Signature：  

```python
def HAND_StartInit(self, hand_id, remote_err):
```

- Parameters：  

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
serial_api_instance.HAND_SetSelfTestLevel(hand_id, 0, [])
err = serial_api_instance.HAND_StartInit(hand_id, [])
assert err == HAND_RESP_SUCCESS, f"test_start_init: {err}\n"
```

### <span style="background-color: #e7f4ffff;color: red;"> HAND_SetManufactureData()</span>

- Method Signature：  

```python
def HAND_SetManufactureData(self, hand_id, key, sub_model, hw_revision, serial_number, customer_tag, remote_err):
```

- Purpose：

  This function configures the manufacturing data of the robotic hand, including critical information such as the product key, sub-model, hardware version, serial number, and customer tag. This data is typically used for device identification, authorization verification, and production traceability.  

- Parameters：

    <table>
    <thead>
        <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code>hand_id</code></td>
        <td>Device Address</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>key</code></td>
        <td>Product Key</td>
        </tr>
        <tr>
        <td><code>sub_model</code></td>
        <td>Submodel</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>hw_revision</code></td>
        <td>Hardware Version</td>
        </tr>
        <tr>
        <td><code>serial_number</code></td>
        <td>Serial Number</td>
        </tr>
        <tr style="background-color: #e6f7ff;">
        <td><code>customer_tag</code></td>
        <td>Customer Tag</td>
        </tr>
        <tr>
        <td><code>remote_err</code></td>
        <td>Remote Error Code Storage</td>
        </tr>
    </tbody>
    </table>

- Return Value:  
Status: None on success  
Failure: Return the corresponding error code

- Usage Example:  

```python
key = [0x88, 0x77]
sub_model = 1
hw_revision = 10
serial_number = [0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F, 0x10]
customer_tag = [0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08]

err = serial_api_instance.HAND_SetManufactureData(hand_id, key, sub_model, hw_revision, serial_number, customer_tag, [])
assert err == HAND_RESP_SUCCESS, f"manufacture_data_set : {err}\n"
```

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**
