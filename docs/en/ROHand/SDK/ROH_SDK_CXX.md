# 👉SDK C/C++

This SDK development kit aims to provide convenient C/C++ interfaces and accompanying sample code for the secondary development of the OYMotion dexterous hand. Through the sample demos, users can easily implement a series of core functions such as precise control of the dexterous hand's fingers, device status monitoring, and flexible parameter configuration, helping developers quickly build applications and shorten the development cycle.  

## 👉Download the SDK

- Method 1: Click this link [ohand_serial_sdk](../../../assets/downloads/ROHand/ohand_serial_sdk-master.zip) to directly download the development kit  

- Method 2: Visit [ohand_serial_sdk_python](https://github.com/oymotion/ohand_serial_sdk){: target="_blank"} Github page to download the latest SDK.  

- Method 3: Obtain via clone:  

    ```Bash
    git clone https://github.com/oymotion/ohand_serial_sdk
    ```

## 👉Introduction to the demos

The following example demos are designed around the core functional development needs of the OYMotion dexterous hand, covering full-scenario applications from basic control to advanced configuration. Each example provides complete and runnable C/C++ code, including clear interface calling logic and process comments. Developers can directly compile and run to verify functions, and can also quickly adapt to their own application scenarios based on the example code.  

### 1. custom_cmd_test

This example program supports UART and CAN ports for device communication, and also supports customized interfaces to achieve high-speed reading and writing of dexterous hand-related control parameters. It is suitable for scenarios that require fine-tuning of device operating parameters and real-time acquisition of core control data, providing underlying parameter operation support for personalized function development.

### 2.grip_exec

This example program implements control of the dexterous hand based on predefined gestures and includes complete functions such as communication establishment and status checking.

### 3.set_id

This example program allows users to set the ID of the dexterous hand by entering an ID number, enabling flexible device management.

### 4.simple_control

This example program supports UART and CAN ports for device communication, achieving simple control of the dexterous hand through cyclic gesture actions via both protocols. The code is lightweight and easy to understand, suitable for developers to quickly familiarize themselves with the dual-protocol communication process and build a basic framework for complex control scenarios.  

## 👉Instructions for Using the Development Kit

### Windows Enviroment for Using Instructions

#### 1. Supported Compilers

- MSVC version: **MSVC 2019/2022**, featuring good compatibility with Windows systems and support for the latest C language standards, which can meet the compilation requirements in development.  

- CMake version: 3.5 or higher  

- C++ version: C++11 or higher

#### 2. Development Kit Description

- **header files**: C/C++ language development kit includes the following header files:
  - <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">log.h</span>: Log header file, provides log level control functions
  - <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">OHandGripExec.h</span>: Defines multiple gestures and provides execution functions for the defined gesture controls

  - <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">OHandSerialAPI.h</span>: Dexterous hand interface header file, defines related functions for dexterous hand operations

- **Dynamic Link Library（DLLs）**: Contains the functions and interfaces required to control the dexterous hand, includes the following two versions:  
  - debug: Debug version for Windows 64-bit compilers, includes debug information, suitable for development phase
  - release: Release version for Windows 64-bit compilers, optimized without debug information, suitable for deployment and execution
  
### Linux Enviroment for Using Instructions

#### 1. Supported Architectures

- **x86**: Standard Intel and AMD processor architectures
- **ARM**: Suitable for ARM architecture processors

#### 2. Compiler

- **GCC**: GNU Compiler Collection（GCC）is a widely used open-source compiler collection for Linux. The compiler requires GCC version 11.4 or higher to ensure optimal performance and compatibility.

#### 3. System Version

- **Ubuntu 22.04**: Based on Ubuntu 22.04 Linux system, includes GCC version 11 or higher compilers

#### 4. Development Kit Description

- **Header files**: Same as Windows header files, for details please refer to the Windows environment development kit documentation
- **库文件(.a文件)**: Contains the functions and interfaces required to control the dexterous hand

## 👉Usage Example-MSVC

Example Project: <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">simple_control</span>, environment preparation:  

- The project path is located under the D: drive partition  

- Visual Studio community 2022 version:  
  - During installation, select "Desktop development with C++"  
  - MSVC 2022 version  

### 1. Explanation

This sample project is developed using Microsoft Visual Studio C/C++, aiming to demonstrate the simple implementation process of programmatically controlling a dexterous hand.

### 2. Install serial Library

Click [serial(github)](https://github.com/wjwwood/serial) or [serial(Offline compressed package)](../../../assets/downloads/ROHand/serial-main.zip) to download the open-source project, open visual_studio/visual_studio.sln in the directory, and compile it. Place the compiled folder in the same partition as this project. Your serial folder structure should look like the following:  

```TXT
d:\serial
├─include
│  └─serial
│      │  serial.h
│      │  v8stdint.h
│      │
│      └─impl
│              unix.h
│              win.h
│
└─lib
    ├─Debug
    │      serial.idb
    │      serial.lib
    │      serial.pdb
    │
    └─Release
            serial.lib
            serial.pdb
```

### 3. Install PCAN-USB Driver

Click [PCAN-USB(Official Website)](https://www.peak-system.com/PCAN-USB.199.0.html?&L=1) to download and install PCAN-USB driver.  

### 4. Install PCAN-Basic Library

Click [PCAN-Basic](https://www.peak-system.com/PCAN-Basic.126.0.html?&L=1) to download and extract the PCAN-Basic library. Place it in the same partition as this project, the path should be as follows:
d:\PCAN-Basic

### 5. Compile

In main.cpp, the protocol type can be modified through the macro definition **PORT_TYPE**, for example:  

- RS485: `PORT_TYPE = PORT_TYPE_UART`
- CAN: `PORT_TYPE = PORT_TYPE_CAN`

Open the command line window and perform the following operations:  

- Enter the project directory and compile  

```BATCH
cd path\to\project
md build
cd build
cmake ..
```

- Compile Debug version  

```BATCH
cmake --build . --config Debug
```

- Compile Release version  

```BATCH
cmake --build . --config Release
```

### 6. Run

Open the command line window and perform the following operations:  

- Enter the Debug or Release directory  

```BATCH
cd path\to\project\build\Debug
```

- run program(serial), Replace COMx with the actual serial port number  

```BATCH
simple_control COMx
```

- run program(can), Replace x with the actual serial port number  

```BATCH
simple_control x
```

## 👉Interface Description

### Header File Protection and External Declarations

防止头文件被重复包含，同时支持 C++ 编译器对 C 代码的兼容处理  

```cpp  
#ifndef __HAND_SERIAL_API_H__
#define __HAND_SERIAL_API_H__

#ifdef __cplusplus
extern "C" {
#endif

#ifdef __cplusplus
}
#endif
#endif //__HAND_SERIAL_API_H__
```

### Basic Type Definitions

```cpp
#ifndef NULL
#define NULL ((void*)0)
#endif

#ifndef BOOL
#define BOOL uint8_t
#endif

#ifndef TRUE
#define TRUE 1
#endif

#ifndef FALSE
#define FALSE 0
#endif
```

### Constant Definitions

```cpp
#define MAX_THUMB_ROOT_POS 3
#define MAX_MOTOR_CNT 6
#define MAX_FORCE_ENTRIES 12 * 5
```

- <span style="background-color: #e7f4ffff;">MAX_THUMB_ROOT_POS</span>: Maximum gear position corresponding to thumb base rotation  
- <span style="background-color: #e7f4ffff;">MAX_MOTOR_CNT</span>: Maximum number of motors  
- <span style="background-color: #e7f4ffff;">MAX_FORCE_ENTRIES</span>: Maximum number of force sensor data entries per single finger  

### Protocol Version

Protocol Major Version Number  

```cpp
#define PROTOCOL_VERSION_MAJOR 3
```

### Enum Definitions

```cpp
typedef enum
{
  HAND_PROTOCOL_UART,
  HAND_PROTOCOL_I2C
} HAND_PROTOCOL;
```

- Defines the communication protocol types supported by the Hand device , including both UART and I2C  

### Error Code Definitions

#### 1. Protocol-Related Errors

```cpp
#define ERR_PROTOCOL_WRONG_LRC                          0x01
```

- <span style="background-color: #e7f4ffff;">ERR_PROTOCOL_WRONG_LRC</span>: LRC Checksum Error  

#### 2. Command-Related Errors

```cpp
#define ERR_COMMAND_INVALID                             0x11
#define ERR_COMMAND_INVALID_BYTE_COUNT                  0x12
#define ERR_COMMAND_INVALID_DATA                        0x13
```

- <span style="background-color: #e7f4ffff;">ERR_COMMAND_INVALID</span>: Invald command  
- <span style="background-color: #e7f4ffff;">ERR_COMMAND_INVALID_BYTE_COUNT</span>: Invalid command byte count  
- <span style="background-color: #e7f4ffff;">ERR_COMMAND_INVALID_DATA</span>: Invalid command data  

#### 3. Status-Related Errors

```cpp
#define ERR_STATUS_INIT                                 0x21
#define ERR_STATUS_CALI                                 0x22
#define ERR_STATUS_STUCK                                0x23
```

- <span style="background-color: #e7f4ffff;">ERR_STATUS_INIT</span>: Initialization status error  
- <span style="background-color: #e7f4ffff;">ERR_STATUS_CALI</span>: Calibration status error  
- <span style="background-color: #e7f4ffff;">ERR_STATUS_STUCK</span>: Motor stuck error  

#### 4. Operation Result Related Errors

```cpp
#define ERR_OP_FAILED                                   0x31
#define ERR_SAVE_FAILED                                 0x32
```

- <span style="background-color: #e7f4ffff;">ERR_OP_FAILED</span>: Operation failed  
- <span style="background-color: #e7f4ffff;">ERR_SAVE_FAILED</span>: Save failed  

### Device Operation Return Value

```cpp
#define HAND_RESP_HAND_ERROR                            0xFF           

#define HAND_RESP_SUCCESS                               0x00
#define HAND_RESP_TIMER_FUNC_NOT_SET                    0x01           
#define HAND_RESP_INVALID_CONTEXT                       0x02           
#define HAND_RESP_TIMEOUT                               0x03          
#define HAND_RESP_INVALID_OUT_BUFFER_SIZE               0x04           
#define HAND_RESP_UNMATCHED_ADDR                        0x05           
#define HAND_RESP_UNMATCHED_CMD                         0x06           
#define HAND_RESP_DATA_SIZE_TOO_BIG                     0x07           
#define HAND_RESP_DATA_INVALID                          0x08           
```

- <span style="background-color: #e7f4ffff;">HAND_RESP_HAND_ERROR</span>: Device error, specific error code needs to be obtained through callback  
- <span style="background-color: #e7f4ffff;">HAND_RESP_SUCCESS</span>: Device response success  
- <span style="background-color: #e7f4ffff;">HAND_RESP_TIMER_FUNC_NOT_SET</span>: Timer function not set, need to call HAND_SetTimerFunction() to set the callback function  
- <span style="background-color: #e7f4ffff;">HAND_RESP_INVALID_CONTEXT</span>: Invalid context, context is NULL or send function is not set  
- <span style="background-color: #e7f4ffff;">HAND_RESP_TIMEOUT</span>: Timeout error, waiting for node response timeout  
- <span style="background-color: #e7f4ffff;">HAND_RESP_INVALID_OUT_BUFFER_SIZE</span>: Output buffer size mismatch  
- <span style="background-color: #e7f4ffff;">HAND_RESP_UNMATCHED_ADDR</span>: Node address mismatch  
- <span style="background-color: #e7f4ffff;">HAND_RESP_UNMATCHED_CMD</span>: Command mismatch  
- <span style="background-color: #e7f4ffff;">HAND_RESP_DATA_SIZE_TOO_BIG</span>: Data size exceeded, sent data exceeds buffer size  
- <span style="background-color: #e7f4ffff;">HAND_RESP_DATA_INVALID</span>: Invalid data content  

### Custom Command Sub-Command Definitions

Used for HAND_SetCustom() to achieve high-speed read/write functionality for dexterous hand related control parameters

```cpp
#define SUB_CMD_SET_SPEED     (1 << 0)
#define SUB_CMD_SET_POS       (1 << 1)
#define SUB_CMD_SET_ANGLE     (1 << 2)
#define SUB_CMD_GET_POS       (1 << 3)
#define SUB_CMD_GET_ANGLE     (1 << 4)
#define SUB_CMD_GET_CURRENT   (1 << 5)
#define SUB_CMD_GET_FORCE     (1 << 6)
#define SUB_CMD_GET_STATUS    (1 << 7)
```

### Create Context <span style="background-color: #e7f4ffff;color: red;">HAND_CreateContext()</span>  

- Method Prototype:  

```cpp
void *HAND_CreateContext(
  const void *ctx_private_data,
  HAND_PROTOCOL protocol,
  uint8_t address_master,
  void (*SendDataImpl)(uint8_t addr, uint8_t *data, uint8_t size, void *ctx),
  void (*RecvDataImpl)(void *ctx)
)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx_private_data</code></td>
        <td>Context private data (such as serial port instance address)</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>protocol</code></td>
        <td>Communication protocol (UART or I2C)</td>
      </tr>
      <tr>
        <td><code>address_master</code></td>
        <td>Master node address</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>SendDataImpl</code></td>
        <td>Send data function pointer</td>
      </tr>
      <tr>
        <td><code>RecvDataImpl</code></td>
        <td>Receive data function pointer</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example  

```cpp
void* port = NULL;
void* hand_ctx = NULL;

void* init(const char* port_name, uint32_t baudrate)
{
  // Serial port initialization code omitted here
  return port;
}

void send_data(uint8_t addr, uint8_t* data, uint8_t len, void* hand_ctx)
{
  // Data transmission logic omitted here
}

void recv_data(void* hand_ctx)
{
  // Data reception logic omitted here
}

port = init(port_name, baud_rate);
hand_ctx = HAND_CreateContext(port, HAND_PROTOCOL_UART, ADDRESS_MASTER, send_data, recv_data);
```

### Free Context <span style="background-color: #e7f4ffff;color: red;">HAND_FreeContext()</span>  

- Method Prototype:  

```cpp
void HAND_FreeContext(void *ctx)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
    <tr>
        <td><code>ctx</code></td>
        <td>OHAND context</td>
      </tr>
    </tbody>
  </table>

- Usage Example  

```cpp
HAND_FreeContext(hand_ctx);
```

### Timer Settings <span style="background-color: #e7f4ffff;color: red;">HAND_SetTimerFunction()</span>  

- Method Prototype:  

```cpp
void HAND_SetTimerFunction(uint32_t (*GetMilliSecondsImpl)(void), void (*DelayMilliSecondsImpl)(uint32_t ms))
```

- Parameter Description:
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>GetMilliSecondsImpl</code></td>
        <td>Function pointer to get milliseconds</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>DelayMilliSecondsImpl</code></td>
        <td>Millisecond delay function pointer</td>
      </tr>
    </tbody>
  </table>  

- Usage Example  

```cpp
uint32_t millis()
{
    chrono::time_point<chrono::system_clock, chrono::milliseconds> tp = chrono::time_point_cast<chrono::milliseconds>(chrono::system_clock::now());
    auto tmp = chrono::duration_cast<chrono::milliseconds>(tp.time_since_epoch());
    time_t timestamp = tmp.count();
    static uint64_t startTime = (uint64_t)timestamp;
    return (uint32_t)(timestamp - startTime);
}

void delay(uint32_t millisecondsToWait)
{
    this_thread::sleep_for(chrono::milliseconds(millisecondsToWait));
}

HAND_SetTimerFunction(millis, delay);
```

### Get Timestamp <span style="background-color: #e7f4ffff;color: red;">HAND_GetTick()</span>  

- Method Prototype:  

```cpp  
uint32_t HAND_GetTick(void)
```

- Usage Example  

```cpp
uint32_t current_tick = HAND_GetTick();
```

### Set Timeout Command <span style="background-color: #e7f4ffff;color: red;">HAND_SetCommandTimeOut()</span>  

- Method Prototype:  

```cpp
void HAND_SetCommandTimeOut(void *ctx, uint16_t timeout)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>timeout</code></td>
        <td>Timeout time (milliseconds)</td>
      </tr>
    </tbody>
  </table>

- Usage Example  

```cpp
HAND_SetCommandTimeOut(hand_ctx, 255); // Set timeout time to 255 milliseconds
```

### Data Processing <span style="background-color: #e7f4ffff;color: red;">HAND_OnData()</span>  

- Method Prototype:  

```cpp
void HAND_OnData(void *ctx, uint8_t data)
```

- Purpose: Feed received data into the internal parser, should be called in the receive function (RecvDataImpl) or interrupt service routine (ISR)

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data</code></td>
        <td>Received byte data</td>
      </tr>
    </tbody>
  </table>

- Usage Example  

```cpp
// Assuming the port used is serial
void RecvData(void *ctx)
{
  uint8_t data = 0;
  auto port = *(serial::Serial**)hand_ctx;
  while (port->available() != 0)
  {
    port->read(&data, 1);
    HAND_OnData(hand_ctx, data);
  }
}
```

### Get Protocol Version <span style="background-color: #e7f4ffff;color: red;">HAND_GetProtocolVersion()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetProtocolVersion(void *ctx, uint8_t hand_id, uint8_t *major, uint8_t *minor, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>major</code></td>
        <td>Device major version number</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>minor</code></td>
        <td>Device minor version number</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example  

```cpp
uint8_t major_ver, minor_ver;
uint8_t remote_err;
uint8_t used_id = 0x02;
test_err = HAND_GetProtocolVersion(hand_ctx, used_id, &major_ver, &minor_ver, &remote_err);
```

### Get Firmware Version<span style="background-color: #e7f4ffff;color: red;">GetFirmwareVersion()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFirmwareVersion(void *ctx, uint8_t hand_id, uint8_t *major, uint8_t *minor, uint16_t *revision, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>major</code></td>
        <td>Device major version number</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>minor</code></td>
        <td>Device minor version number</td>
      </tr>
      <tr>
        <td><code>revision</code></td>
        <td>Device revision version number</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example  

```cpp
uint8_t major_ver, minor_ver;
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t revision;
test_err = HAND_GetFirmwareVersion(hand_ctx, used_id, &major_ver, &minor_ver, &revision, &remote_err);
```

### Get Hardware Version <span style="background-color: #e7f4ffff;color: red;">HAND_GetHardwareVersion()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetHardwareVersion(void *ctx, uint8_t hand_id, uint8_t *hw_type, uint8_t *hw_ver, uint16_t *boot_version, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>hw_type</code></td>
        <td>Device hardware type</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hw_ver</code></td>
        <td>Device hardware version number</td>
      </tr>
      <tr>
        <td><code>boot_version</code></td>
        <td>Device bootloader version number</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example  

```cpp
uint8_t hw_type, hw_ver;
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t boot_version;
test_err = HAND_GetHardwareVersion(hand_ctx, used_id, &hw_type, &hw_ver, &boot_version, &remote_err);
```

### Get Calibration Data <span style="background-color: #e7f4ffff;color: red;">HAND_GetCaliData()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetCaliData(void *ctx, uint8_t hand_id, uint16_t *end_pos, uint16_t *start_pos, uint8_t *motor_cnt, uint16_t *thumb_root_pos, uint8_t *thumb_root_pos_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>end_pos</code></td>
        <td>Storage of endpoint position array</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>start_pos</code></td>
        <td>Storage of startpoint position array</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>thumb_root_pos</code></td>
        <td>Gear position array for thumb base location(0, 1, 2)</td>
      </tr>
      <tr>
        <td><code>thumb_root_pos_cnt</code></td>
        <td>Number of gear positions at the thumb base location</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t end_pos[NUM_MOTORS];
uint16_t start_pos[NUM_MOTORS];
uint8_t motor_cnt = NUM_MOTORS;
uint16_t thumb_root_pos[3];
uint8_t  thumb_root_pos_cnt = 3;
test_err = HAND_GetCaliData(hand_ctx, used_id, end_pos, start_pos, &motor_cnt, thumb_root_pos, &thumb_root_pos_cnt, &remote_err);
```

### Get finger PID <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerPID(void *ctx, uint8_t hand_id, uint8_t finger_id, float *p, float *i, float *d, float *g, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>finger id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>Proportional coefficient</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>Integral coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>Differential coefficient</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>Gain coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
float p, i, d, g;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerPID(hand_ctx, used_id, finger_index, &p, &i, &d, &g, &remote_err);
}
```

### Get Finger Current Limit <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerCurrentLimit()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerCurrentLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *current_limit, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
        <tr>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_limit</code></td>
        <td>Current limit</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t current_limit;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerCurrentLimit(hand_ctx, used_id, finger_index, &current_limit, &remote_err);
}
```

### Get Finger Current <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerCurrent()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerCurrent(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *current, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current</code></td>
        <td>Finger current</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t current;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerCurrent(hand_ctx, used_id, finger_index, &current, &remote_err);
}
```

### Get Finger Force Target <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerForceTarget()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerForceTarget(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *force_target, uint8_t *remote_err)
```

- Purpose: Get the target force value setting for the specified finger, which is used for closed-loop control in force control mode (i.e., the device will automatically adjust motor output to maintain this target force)  

- Paramter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Paramter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  ID</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force_target</code></td>
        <td>Finger force target value</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t force_target;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerForceTarget(hand_ctx, used_id, finger_index, &force_target, &remote_err);
}
```

### Get Finger Force Sensor Data <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerForce()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerForce(void *ctx, uint8_t hand_id, uint8_t finger_id, uint8_t *force_entry_cnt, uint8_t *force, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force_entry_cnt</code></td>
        <td>Force data entry count</td>
      </tr>
      <tr>
        <td><code>force</code></td>
        <td>Storage variable address for force data, capable of storing multi-point force values, or normal force, tangential force and direction</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
#define MAX_FORCE_ENTRIES 12 * 5 /* Max force entries for one finger */
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t force[MAX_FORCE_ENTRIES] = { 0 };
uint8_t force_entry_count;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 force_entry_count = force_entries[finger_index];
 delay(100);
 test_err = HAND_GetFingerForce(hand_ctx, used_id, finger_index, &force_entry_count, force, &remote_err);
}
```

### Get Finger Absolute Position Limit Values <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosLimit()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerPosLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *low_limit, uint16_t *high_limit, uint8_t *remote_err)
```

- Purpose: Get the absolute position limit range for the specified finger, used to constrain the finger's movement range  

- Paramter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Paramter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device  id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>low_limit</code></td>
        <td>Position lower limit value</td>
      </tr>
      <tr>
        <td><code>high_limit</code></td>
        <td>Position upper limit value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error code</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t low_limit, high_limit;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerPosLimit(hand_ctx, used_id, finger_index, &low_limit, &high_limit, &remote_err);
}
```

### Get Finger Absolute Position <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosAbs()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerPosAbs(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_pos</code></td>
        <td>Target absolute position</td>
      </tr>
      <tr>
        <td><code>current_pos</code></td>
        <td>Current absolute position</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t target_pos, current_pos;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerPosAbs(hand_ctx, used_id, finger_index, &target_pos, &current_pos, &remote_err);
}
```

### Get Finger Logical Position <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPos()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerPos(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_pos</code></td>
        <td>Logical target position</td>
      </tr>
      <tr>
        <td><code>current_pos</code></td>
        <td>Logical current position</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t target_pos, current_pos;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerPos(hand_ctx, used_id, finger_index, &target_pos, &current_pos, &remote_err);
}
```

### Get Finger Angle <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerAngle()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerAngle(void *ctx, uint8_t hand_id, uint8_t finger_id, int16_t *target_angle, int16_t *current_angle, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_angle</code></td>
        <td>Target angle value, unit: actual angle * 100</td>
      </tr>
      <tr>
        <td><code>current_angle</code></td>
        <td>Current angle value, unit: actual angle * 100</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
int16_t target_angle, current_angle;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
 delay(100);
 test_err = HAND_GetFingerAngle(hand_ctx, used_id, finger_index, &target_angle, &current_angle, &remote_err);
}
```

### Get Thumb Base Gear Position <span style="background-color: #e7f4ffff;color: red;">HAND_GetThumbRootPos()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetThumbRootPos(void *ctx, uint8_t hand_id, uint16_t *raw_encoder, uint8_t *pos, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>raw_encoder</code></td>
        <td>Finger base raw encoder value, range: 0~65535</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos</code></td>
        <td>Thumb base mapped position, range: 0~2 three gear positions</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t raw_encoder;
uint8_t pos;
test_err = HAND_GetThumbRootPos(hand_ctx, used_id, &raw_encoder, &pos, &remote_err);
```

### Get All Finger Absolute Positions <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosAbsAll()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerPosAbsAll(void *ctx, uint8_t hand_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>target_pos</code></td>
        <td>Array of target absolute positions for all fingers/td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_pos</code></td>
        <td>Array of current absolute positions for all fingers</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
uint16_t raw_target_pos[NUM_MOTORS], raw_current_pos[NUM_MOTORS];
test_err = HAND_GetFingerPosAbsAll(hand_ctx, used_id, raw_target_pos, raw_current_pos, &motor_cnt, &remote_err);
```

### 获取所有手指逻辑位置<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosAll()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerPosAll(void *ctx, uint8_t hand_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>target_pos</code></td>
        <td>Array of target logical positions for all fingers/td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_pos</code></td>
        <td>Array of current logical positions for all fingers</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t raw_target_pos[NUM_MOTORS], raw_current_pos[NUM_MOTORS];
uint8_t motor_cnt = NUM_MOTORS;
test_err = HAND_GetFingerPosAll(hand_ctx, used_id, raw_target_pos, raw_current_pos, &motor_cnt, &remote_err);
```

### Get All Finger Angles <span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerAngleAll()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetFingerAngleAll(void *ctx, uint8_t hand_id, int16_t *target_angle, int16_t *current_angle, uint8_t *motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>target_angle</code></td>
        <td>Array of target angle values for all fingers, unit: actual angle * 100/td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_angle</code></td>
        <td>Array of current angle values for all fingers, unit: actual angle * 100</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
int16_t raw_target_angle[NUM_MOTORS], raw_current_angle[NUM_MOTORS];
test_err = HAND_GetFingerAngleAll(hand_ctx, used_id, raw_target_angle, raw_current_angle, &motor_cnt, &remote_err);
```

### Get Self-test Level <span style="background-color: #e7f4ffff;color: red;">HAND_GetSelfTestLevel()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetSelfTestLevel(void *ctx, uint8_t hand_id, uint8_t *self_test_level, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>self_test_level</code></td>
        <td>Self-test level: 0.No automatic self-test, 1.Automatic partial self-test, 2.Automatic comprehensive self-test</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t self_test_level;
test_err = HAND_GetSelfTestLevel(hand_ctx, used_id, &self_test_level, &remote_err);
```

### Get Beep Switch Status <span style="background-color: #e7f4ffff;color: red;">HAND_GetBeepSwitch()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetBeepSwitch(void *ctx, uint8_t hand_id, uint8_t *beep_switch, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>beep_switch</code></td>
        <td>Beep switch status: 0.Off, 1.On</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t beep_switch;
uint8_t remote_err;
uint8_t used_id = 0x02;
test_err = HAND_GetBeepSwitch(hand_ctx, used_id, &beep_switch, &remote_err);
```

### Get UID <span style="background-color: #e7f4ffff;color: red;">HAND_GetUID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetUID(void *ctx, uint8_t hand_id, uint32_t *uid_w0, uint32_t *uid_w1, uint32_t *uid_w2, uint8_t *remote_err)
```

- Purpose: Get the 96-bit unique identifier (UID) of the Hand device, used for device identification, uniqueness verification and other scenarios  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>uid_w0</code></td>
        <td>Device UID Word 0</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>uid_w1</code></td>
        <td>Device UID Word 1</td>
      </tr>
      <tr>
        <td><code>uid_w0</code></td>
        <td>Device UID Word 2</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint32_t uid_w0, uid_w1, uid_w2;
test_err = HAND_GetUID(hand_ctx, used_id, &uid_w0, &uid_w1, &uid_w2, &test_remote_err);
```

### Get Manufacture Data<span style="background-color: #e7f4ffff;color: red;">HAND_GetManufactureData()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetManufactureData(void *ctx, uint8_t hand_id, uint8_t *data, uint8_t *data_size, uint8_t *remote_err)
```

- Purpose: Get the manufacturer data of the Hand device, typically containing production-related information (such as production batch, verification information, etc.)  
  
- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>data</code></td>
        <td>Manufacturer Data</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data_size</code></td>
        <td>Actual length of manufacturer data</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t data_size = 26;
uint8_t* data = (uint8_t*)malloc(data_size * sizeof(uint8_t));
test_err = HAND_GetManufactureData(hand_ctx, used_id, data, &data_size, &test_remote_err);
```

### GetVendor ID<span style="background-color: #e7f4ffff;color: red;">HAND_GetVendorID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetVendorID(void *ctx, uint8_t hand_id, uint16_t *vendor_id, uint8_t *remote_err)
```

- Purpose: Get the Vendor ID of the Hand device, used to identify the device manufacturer, typically a unique identifier exclusive to the manufacturer  
  
- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>vendor_id</code></td>
        <td>厂商ID</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint16_t vendor_id;
test_err = HAND_GetVendorID(hand_ctx, used_id, &vendor_id, &test_remote_err);
```

### Get Finger Force PID Parameter<span style="background-color: #e7f4ffff;color: red;">HAND_GetForcePID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetForcePID(void *ctx, uint8_t hand_id, uint8_t finger_id, float *p, float *i, float *d, float *g, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>Proportional coefficient</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>Integral coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>Derivative coefficient</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>Gain coefficient</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_FINGERS 5
uint8_t remote_err;
uint8_t used_id = 0x02;
float p, i, d, g;
for (int fingerIndex = 0; fingerIndex < NUM_FINGERS; fingerIndex++) {
 delay(100);
 test_err = HAND_GetForcePID(hand_ctx, used_id, fingerIndex, &p, &i, &d, &g, &remote_err);
}
```

### Reset device <span style="background-color: #e7f4ffff;color: red;">HAND_Reset()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_Reset(void *ctx, uint8_t hand_id, uint8_t mode, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>mode</code></td>
        <td>Reset mode (0: Boot to user code; 1: Boot to DFU mode)</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t mode = 0;
test_err = HAND_Reset(hand_ctx, used_id, 0, &remote_err);
```

### Set id <span style="background-color: #e7f4ffff;color: red;">HAND_SetID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetID(void *ctx, uint8_t hand_id, uint8_t new_id, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>new_id</code></td>
        <td>New device ID</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t new_id = 0x03;
test_err = HAND_SetID(hand_ctx, used_id, new_id, &remote_err);
```

### Enter calibration mode <span style="background-color: #e7f4ffff;color: red;">HAND_Calibrate()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_Calibrate(void *ctx, uint8_t hand_id, uint16_t key, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>key</code></td>
        <td>Calibration Key</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**

### Get Battery Voltage<span style="background-color: #e7f4ffff;color: red;">HAND_GetBatteryVoltage()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetBatteryVoltage(void *ctx, uint8_t hand_id, uint16_t *voltage, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>voltage</code></td>
        <td>Battery voltage</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This function is only available for bionic hands, not supported for dexterous hands.**

### Get usage status <span style="background-color: #e7f4ffff;color: red;">HAND_GetUsageStat()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_GetUsageStat(void *ctx, uint8_t hand_id, uint32_t *total_use_time, uint32_t *total_open_times, uint8_t motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
    <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>total_use_time</code></td>
        <td>Total usage time of the device</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>total_open_times</code></td>
        <td>Total open count of each motor</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This function is only available for bionic hands, not supported for dexterous hands.**

### Power off <span style="background-color: #e7f4ffff;color: red;">HAND_PowerOff()</span>  

- Method Prototype:

```cpp
uint8_t HAND_PowerOff(void *ctx, uint8_t hand_id, uint8_t *remote_err)
```  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This function is only available for bionic hands, not supported for dexterous hands.**

### Set Calibration Data <span style="background-color: #e7f4ffff;color: red;">HAND_SetCaliData()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetCaliData(void *ctx, uint8_t hand_id, uint16_t *end_pos, uint16_t *start_pos, uint8_t motor_cnt, uint16_t *thumb_root_pos, uint8_t thumb_root_pos_cnt, uint8_t *remote_err)
```  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>end_pos</code></td>
        <td>Endpoint position calibration data for each motor</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>start_pos</code></td>
        <td>Start point position calibration data for each motor</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>thumb_root_pos</code></td>
        <td>Preset position calibration data for the thumb base</td>
      </tr>
      <tr>
        <td><code>thumb_root_pos_cnt</code></td>
        <td>Number of preset positions for the thumb base</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**

### Set finger PID Parameter <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerPID(void *ctx, uint8_t hand_id, uint8_t finger_id, float p, float i, float d, float g, uint8_t *remote_err)
```  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>Proportional coefficient</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>Integral coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>Derivative coefficient</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>Gain coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>  

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
static const float _pidGains[][4] = {
  {250.00, 2.00, 250.00, 1.00},
  {250.00, 2.00, 250.00, 1.00},
  {250.00, 2.00, 250.00, 1.00},
  {250.00, 2.00, 250.00, 1.00},
  {250.00, 2.00, 250.00, 1.00},
  {250.00, 2.00, 250.00, 1.00}
};
for (int i = 0; i < NUM_MOTORS; i++){
  err = HAND_SetFingerPID(hand_ctx, used_id, i, _pidGains[i][0], _pidGains[i][1], _pidGains[i][2], _pidGains[i][3], &remote_err);
}
```  

### Set Finger Current Limit Value <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerCurrentLimit()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerCurrentLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t current_limit, uint8_t *remote_err)
```  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_limit</code></td>
        <td>Current limit value</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>  

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t current_limit_set = 200;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  test_err = HAND_SetFingerCurrentLimit(hand_ctx, used_id, finger_index, current_limit_set, &remote_err);
}
```  

### Set Finger Force Feedback Target Value <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerForceTarget()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerForceTarget(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t force_target, uint8_t *remote_err)
```

- Purpose: Set the target force value for the specified finger, which is used for closed-loop control in force control mode (i.e., the device will automatically adjust motor output to maintain this target force)  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force_target</code></td>
        <td>Target force value, unit: mN</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>  

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t force_target_set = 200;
for (int finger_index = 0; finger_index < NUM_FINGERS; finger_index++) {
  test_err = HAND_SetFingerForceTarget(hand_ctx, used_id, finger_index, force_target_set, &remote_err);
}
```

### Set Finger Absolute position Limit Value <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosLimit()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerPosLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t low_limit, uint16_t high_limit, uint8_t *remote_err)
```  

- Purpose: Set the absolute position limit range for the specified finger, used to constrain the finger's movement range  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>low_limit</code></td>
        <td>Absolute position lower limit value</td>
      </tr>
      <tr>
        <td><code>high_limit</code></td>
        <td>Absolute position upper limit value</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t low_limit_set = 3800, high_limit_set = 16000;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  test_err = HAND_SetFingerPosLimit(hand_ctx, used_id, finger_index, low_limit_set, high_limit_set, &remote_err);
}
```

### Activate finger (when stuck) <span style="background-color: #e7f4ffff;color: red;">HAND_FingerStart()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_FingerStart(void *ctx, uint8_t hand_id, uint8_t finger_id_bits, uint8_t *remote_err)
```  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id_bits</code></td>
        <td>Finger corresponding bitmask</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
const uint8_t finger_ids[NUM_MOTORS] = { 1, 2, 4, 6, 8, 10 };
for (int i = 0; i < NUM_MOTORS; i++) {
  test_err = HAND_FingerStart(hand_ctx, used_id, finger_index, &remote_err);
}

```

### Stop finger <span style="background-color: #e7f4ffff;color: red;">HAND_FingerStop()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_FingerStop(void *ctx, uint8_t hand_id, uint8_t finger_id_bits, uint8_t *remote_err)
```  

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id_bits</code></td>
        <td>Finger corresponding bitmask</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
const uint8_t finger_ids[NUM_MOTORS] = { 1, 2, 4, 6, 8, 10 };
for (int i = 0; i < NUM_MOTORS; i++) {
  test_err = HAND_FingerStop(hand_ctx, used_id, finger_index, &remote_err);
}

```

### Set Finger Absolute Position <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosAbs()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerPosAbs(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t raw_pos, uint8_t speed, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>raw_pos</code></td>
        <td>Finger absolute position</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Finger movement speed</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t speed = 255;
uint16_t abs_pos_set = 16000;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  test_err = HAND_SetFingerPosAbs(hand_ctx, used_id, finger_index, abs_pos_set, speed, &remote_err);
}
```

### Set Finger Logical Position <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPos()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerPos(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t pos, uint8_t speed, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos</code></td>
        <td>目标逻辑位置</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Finger movement speed</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t speed = 255;
uint16_t pos_set = 58000;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  test_err = HAND_SetFingerPos(hand_ctx, used_id, finger_index, pos_set, speed, &remote_err);
}
```

### Set Finger Angle <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerAngle()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerAngle(void *ctx, uint8_t hand_id, uint8_t finger_id, int16_t angle, uint8_t speed, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>angle</code></td>
        <td>Target angle value, value is actual angle * 100</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>Finger movement speed</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t speed = 255;
uint16_t four_finger_angle_set = 12000;
uint16_t thumb_angle_set = 1500;
uint16_t thumb_root_angle_set = 6000;

for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  if (finger_index >= 1 && finger_index <= 4) {
  test_err = HAND_SetFingerAngle(hand_ctx, used_id, finger_index, four_finger_angle_set, speed, &remote_err);
 }
 else if (finger_index == 0) {
  test_err = HAND_SetFingerAngle(hand_ctx, used_id, finger_index, thumb_angle_set, speed, &remote_err);
 }
 else {
  test_err = HAND_SetFingerAngle(hand_ctx, used_id, finger_index, thumb_root_angle_set, speed, &remote_err);
 }
}
```

### Set Thumb Base Position <span style="background-color: #e7f4ffff;color: red;">HAND_SetThumbRootPos()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetThumbRootPos(void *ctx, uint8_t hand_id, uint8_t pos, uint8_t speed, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>pos</code></td>
        <td>Target position of thumb base, can only be 0, 1, or 2</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>Finger movement speed</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t speed = 255;
uint8_t pos_set = 1
test_err = HAND_SetThumbRootPos(hand_ctx, used_id, pos_set, speed, &remote_err);
```

### Set All Finger Absolute Positions <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosAbsAll()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerPosAbsAll(void *ctx, uint8_t hand_id, uint16_t *raw_pos, uint8_t *speed, uint8_t motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>raw_pos</code></td>
        <td>All finger absolute position array</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>All Finger movement speed array</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t raw_speed[NUM_MOTORS] = { 100,100,100,100,100,100 };
uint16_t raw_pos_abs[NUM_MOTORS] = { 13000, 13000, 13000, 13000, 13000, 5000 };
uint8_t motor_cnt = NUM_MOTORS;
test_err = HAND_SetFingerPosAbsAll(hand_ctx, used_id, raw_pos_abs, raw_speed, NUM_MOTORS, &remote_err);
```

### Set All Finger Logical Positions <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosAll()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerPosAll(void *ctx, uint8_t hand_id, uint16_t *pos, uint8_t *speed, uint8_t motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>pos</code></td>
        <td>Array of target logical positions for all fingers</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>All Finger movement speed array</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
uint16_t raw_pos[NUM_MOTORS] = { 18000, 33000, 33000, 33000, 33000, 38000 };
test_err = HAND_SetFingerPosAll(hand_ctx, used_id, raw_pos, raw_speed, NUM_MOTORS, &remote_err);
```

### Set All Finger Angles <span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerAngleAll()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerAngleAll(void *ctx, uint8_t hand_id, int16_t *angle, uint8_t *speed, uint8_t motor_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>angle</code></td>
        <td>Array of target angles for all fingers</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>All Finger movement speed array</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>Motor count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
int16_t raw_angle[NUM_MOTORS] = { 2000,12000,12000,12000,12000,5000 };
test_err = HAND_SetFingerAngleAll(hand_ctx, used_id, raw_angle, raw_speed, NUM_MOTORS, &remote_err);
```

### Custom Command, High-speed Read/Write <span style="background-color: #e7f4ffff;color: red;">HAND_SetCustom()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetCustom(void *ctx, uint8_t hand_id, uint8_t* data, uint8_t send_data_size, uint8_t *recv_data_size, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>data</code></td>
        <td>Specific content data of custom command</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>send_data_size</code></td>
        <td>Length of data to be sent</td>
      </tr>
      <tr>
        <td><code>recv_data_size</code></td>
        <td>Length of data to be received</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  
For details, please refer to the example project in this SDK [custom_cmd_test](https://github.com/oymotion/ohand_serial_sdk/tree/master/example/custom_cmd_test){: target="_blank"}

### Set Self-test Level <span style="background-color: #e7f4ffff;color: red;">HAND_SetSelfTestLevel()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetSelfTestLevel(void *ctx, uint8_t hand_id, uint8_t self_test_level, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>self_test_level</code></td>
        <td>Self-test level, 0: No automatic self-test, 1: Partial self-test, 2: Full self-test</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t self_test_level_set = 2;
test_err = HAND_SetSelfTestLevel(hand_ctx, used_id, self_test_level_set, &remote_err);
```

### Set Beep Switch <span style="background-color: #e7f4ffff;color: red;">HAND_SetBeepSwitch()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetBeepSwitch(void *ctx, uint8_t hand_id, uint8_t beep_on, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>beep_on</code></td>
        <td>Beep switch status, 0: Off, 1: On</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t beep_on = 1;
test_err = HAND_SetBeepSwitch(hand_ctx, used_id, beep_on, &remote_err);
```

### Beep <span style="background-color: #e7f4ffff;color: red;">HAND_Beep()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_Beep(void *ctx, uint8_t hand_id, uint16_t duration, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>duration</code></td>
        <td>Duration, unit: ms</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t duration = 200;
test_err = HAND_Beep(hand_ctx, used_id, duration, &remote_err);
```

### Set Button Press Count <span style="background-color: #e7f4ffff;color: red;">HAND_SetButtonPressedCnt()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetButtonPressedCnt(void *ctx, uint8_t hand_id, uint8_t pressed_cnt, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>pressed_cnt</code></td>
        <td>Button press count</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This function is only available for bionic hands, not supported for dexterous hands.**
  
### Trigger initialization (condition: self-test mode is 0) <span style="background-color: #e7f4ffff;color: red;">HAND_StartInit()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_StartInit(void *ctx, uint8_t hand_id, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  
  
- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
HAND_SetSelfTestLevel(hand_ctx, used_id, 0, &remote_err);
test_err = HAND_StartInit(hand_ctx, used_id, &remote_err);
```

### Set Manufacture Data <span style="background-color: #e7f4ffff;color: red;">HAND_SetManufactureData()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetManufactureData(void *ctx, uint8_t hand_id, uint8_t *data, uint8_t data_size, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>data</code></td>
        <td>Manufacture Data</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data_size</code></td>
        <td>Manufacturer data size</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- **Note: This feature is currently not publicly available. Please contact technical support if you need to use this function.**
  
### 设置手指力控PIDParameter<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerForcePID()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_SetFingerForcePID(void *ctx, uint8_t hand_id, uint8_t finger_id, float p, float i, float d, float g, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>Finger id </td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>Proportional coefficient</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>Integral coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>Derivative coefficient</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>Gain coefficient</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>  

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
#define NUM_FINGERS 5
uint8_t remote_err;
uint8_t used_id = 0x02;
float force_pid[][4] = {
 {200.00, 2.00, 98.00, 0.07},
 {200.00, 2.00, 98.00, 0.07},
 {200.00, 2.00, 98.00, 0.07},
 {200.00, 2.00, 98.00, 0.07},
 {200.00, 2.00, 98.00, 0.07},
};
for (int finger_index = 0; finger_index < NUM_FINGERS; finger_index++){
  test_err = HAND_SetFingerForcePID(hand_ctx, used_id, finger_index, force_pid[finger_index][0], force_pid[finger_index][1],force_pid[finger_index][2], force_pid[finger_index][3], &remote_err);
}
```

### Reset Force Sensor Data <span style="background-color: #e7f4ffff;color: red;">HAND_ResetForce()</span>  

- Method Prototype:  

```cpp
uint8_t HAND_ResetForce(void *ctx, uint8_t hand_id, uint8_t *remote_err)
```

- Parameter Description:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>Parameter</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand context</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>Hand device id</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>Remote error cod</td>
      </tr>
    </tbody>
  </table>

- Return Value:  
Success: Returns context pointer  
Failure: Returns NULL  

- Usage Example:  

```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
test_err = HAND_ResetForce(hand_ctx, used_id, &remote_err);
```
