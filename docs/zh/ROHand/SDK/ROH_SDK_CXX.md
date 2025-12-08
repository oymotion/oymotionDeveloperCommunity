# 👉SDK C/C++

本SDK开发包旨在为傲意灵巧手的二次开发提供便捷的C/C++接口与配套示例代码. 通过示例代码, 用户能够轻松实现对灵巧手的手指精准控制、设备状态监控、参数灵活配置等一系列核心功能, 助力开发者快速搭建应用、缩短开发周期.  

## 👉下载SDK

- 方法一: [点击此链接](../../../assets/downloads/ROHand/ohand_serial_sdk-master.zip)下载

- 方法二: 访问[ohand_serial_sdk_python](https://github.com/oymotion/ohand_serial_sdk){: target="_blank"} github网址下载最新版本  

- 方法三: 通过clone获取:  

    ```Bash
    git clone https://github.com/oymotion/ohand_serial_sdk
    ```

## 👉示例简介

以下示例程序围绕傲意灵巧手核心功能开发需求设计，覆盖从基础控制到进阶配置的全场景应用. 每个示例均提供完整可运行的 C/C++ 代码，包含清晰的接口调用逻辑与流程注释，开发者可直接编译运行验证功能，也能基于示例代码快速适配自身应用场景.  

### 1. custom_cmd_test

该示例程序支持UART与CAN端口与设备通讯, 支持客制化接口, 实现高速读写灵巧手相关控制参数功能. 适用于需要精细调整设备运行参数、实时获取核心控制数据的场景，为个性化功能开发提供底层参数操作支持.

### 2.grip_exec

该示例程序基于已定义的手势实现了对灵巧手的控制, 包含了完整的通讯建立和状态检查等功能.

### 3.set_id

该示例程序允许用户通过输入ID号来设置灵巧手的ID, 实现灵活的设备管理.

### 4.simple_control

该示例程序支持UART与CAN端口与设备通讯, 通过循环手势动作实现了双协议对灵巧手简单的控制. 代码轻量化、易理解，适合开发者快速熟悉双协议通讯流程，为复杂控制场景搭建基础框架.  

## 👉开发包使用说明

### Windows环境使用说明

#### 1. 支持的编译器

- MSVC版本: **MSVC 2019/2022版本**, 与Windows系统兼容性好,且支持最新的C语言标准, 能满足开发中的编译需求.  

- cmake 版本: 3.5及以上  

- c++ 版本: c++11及以上

#### 2. 开发包说明

- **头文件**: C语言开发包含以下头文件:
  - <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">log.h</span>: 日志模块头文件, 提供了日志级别控制函数  

  - <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">OHandGripExec.h</span>: 定义了多种手势, 为已定义的手势控制提供了执行函数  

  - <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">OHandSerialAPI.h</span>: 灵巧手接口头文件, 定义了灵巧手操作的相关函数

- **动态链接库（DLLs）**: 包含了控制灵巧手所需的函数和接口, 包含了以下两个版本:  
  - debug: 适用Windows 64位编译器的调试版本，包含调试信息，适合开发阶段使用  

  - release: 适用Windows 64位编译器的发布版本，经过优化，不含调试信息，适合部署运行
  
### Linux环境使用说明

#### 1. 支持的架构

- **x86**: 标准的Intel和AMD处理器架构  

- **ARM**: 适用于ARM架构的处理器

#### 2. 编译器

- **GCC**: GNU Compiler Collection（GCC）是Linux下广泛使用的开源编译器集合. 编译器要求GCC版本为11.4及以上版本, 以确保最佳的性能和兼容性

#### 3. 系统版本

- **Ubuntu 22.04**: 基于Ubuntu 22.04的Linux系统, 包含了GCC 11版本及以上的编译器

#### 4. 开发包说明

- **头文件**: 与Windows头文件相同, 详情见Windows环境的开发包说明  

- **库文件(.a文件)**: 包含了控制灵巧手所需的函数和接口

## 👉使用示例-MSVC

示例项目: <span style="background-color: #f0f0f0; color: red; padding: 2px 4px; border-radius: 2px;">simple_control</span>, 环境准备:  

- 项目路径位于d 盘分区下  

- Visual Studio community 2022 版本:  
  - 在安装时, 选择安装使用C++的桌面开发  
  
  - MSVC 2022版本

### 1. 说明

本示例项目使用Microsoft Visual Studio C/C++开发, 旨在演示程序控制灵巧手的简单实现过程.

### 2. 安装serial库

点击此链接[serial](https://github.com/wjwwood/serial) 或 [serial(离线压缩包)](../../../assets/downloads/ROHand/serial-main.zip) 下载开源项目, 打开在目录下的visual_studio/visual_studio.sln, 然后编译. 将编译好的文件夹放于与该项目相同的分区下, 您的serial文件夹结构应该如下所示:  

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

### 3. 安装PCAN-USB驱动

点击此链接[PCAN-USB](https://www.peak-system.com/PCAN-USB.199.0.html?&L=1)下载并安装PCAN-USB驱动.  

### 4. 安装PCAN-Basic库

点击此链接[PCAN-Basic](https://www.peak-system.com/PCAN-Basic.126.0.html?&L=1)下载并解压PCAN-Basic库. 将其置于与该项目相同的分区下, 路径应如下所示:
d:\PCAN-Basic

### 5. 编译

在main.cpp中可通过宏定义**PORT_TYPE**来修改协议类型, 如:  

- RS485: `PORT_TYPE = PORT_TYPE_UART`  

- CAN: `PORT_TYPE = PORT_TYPE_CAN`

打开命令行窗口, 执行以下操作:  

- 进入项目目录并编译  
```BATCH
cd path\to\project
md build
cd build
cmake ..
```

- 编译Debug版本  

```BATCH
cmake --build . --config Debug
```

- 编译Release版本  

```BATCH
cmake --build . --config Release

```

### 6. 运行

打开命令窗口, 执行以下操作:  

- 进入Debug或Release目录  

```BATCH
cd path\to\project\build\Debug
```

- 运行程序(serial), 将COMx替换为实际的串口号  

```BATCH
simple_control COMx
```

- 运行程序(can), 将x替换为1-16的实际的can口号  

```BATCH
simple_control x
```

## 👉接口说明

### 头文件保护与外部声明

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

### 基础类型定义

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

### 常量定义

```cpp
#define MAX_THUMB_ROOT_POS 3
#define MAX_MOTOR_CNT 6
#define MAX_FORCE_ENTRIES 12 * 5 /* Max force entries for one finger */
```

- <span style="background-color: #e7f4ffff;">MAX_THUMB_ROOT_POS</span>: 大拇指根部旋转对应的最大挡位  

- <span style="background-color: #e7f4ffff;">MAX_MOTOR_CNT</span>: 最大电机数量  

- <span style="background-color: #e7f4ffff;">MAX_FORCE_ENTRIES</span>: 单根手指最大力传感器数据条目数  

### 协议版本

协议主版本号  

```cpp
#define PROTOCOL_VERSION_MAJOR 3
```

### 枚举定义

```cpp
typedef enum
{
  HAND_PROTOCOL_UART,
  HAND_PROTOCOL_I2C
} HAND_PROTOCOL;
```

- 定义手部设备支持的通信协议类型，包括 UART 和 I2C 两种  

### 错误代码定义

#### 1. 协议相关错误

```cpp
#define ERR_PROTOCOL_WRONG_LRC                          0x01
```

- <span style="background-color: #e7f4ffff;">ERR_PROTOCOL_WRONG_LRC</span>: LRC校验错误  

#### 2. 命令相关错误

```cpp
#define ERR_COMMAND_INVALID                             0x11
#define ERR_COMMAND_INVALID_BYTE_COUNT                  0x12
#define ERR_COMMAND_INVALID_DATA                        0x13
```

- <span style="background-color: #e7f4ffff;">ERR_COMMAND_INVALID</span>: 无效命令  

- <span style="background-color: #e7f4ffff;">ERR_COMMAND_INVALID_BYTE_COUNT</span>: 命令字节数无效  

- <span style="background-color: #e7f4ffff;">ERR_COMMAND_INVALID_DATA</span>: 命令数据无效  

#### 3. 状态相关错误

```cpp
#define ERR_STATUS_INIT                                 0x21
#define ERR_STATUS_CALI                                 0x22
#define ERR_STATUS_STUCK                                0x23
```

- <span style="background-color: #e7f4ffff;">ERR_STATUS_INIT</span>: 初始化状态错误  

- <span style="background-color: #e7f4ffff;">ERR_STATUS_CALI</span>: 校准状态错误  

- <span style="background-color: #e7f4ffff;">ERR_STATUS_STUCK</span>: 电机卡住错误  

#### 4. 操作结果相关错误

```cpp
#define ERR_OP_FAILED                                   0x31
#define ERR_SAVE_FAILED                                 0x32
```

- <span style="background-color: #e7f4ffff;">ERR_OP_FAILED</span>: 操作失败  

- <span style="background-color: #e7f4ffff;">ERR_SAVE_FAILED</span>: 保存失败  

### 设备操作返回值

```cpp
#define HAND_RESP_HAND_ERROR                            0xFF           /* device error, error call back will be called with OHand error codes listed above */

#define HAND_RESP_SUCCESS                               0x00
#define HAND_RESP_TIMER_FUNC_NOT_SET                    0x01           /* local error, timer function not set, call HAND_SetTimerFunction(...) first */
#define HAND_RESP_INVALID_CONTEXT                       0x02           /* local error, invalid context, NULL or send data function not set */
#define HAND_RESP_TIMEOUT                               0x03           /* local error, time out when waiting node response */
#define HAND_RESP_INVALID_OUT_BUFFER_SIZE               0x04           /* local error, out buffer size not matched to returned data */
#define HAND_RESP_UNMATCHED_ADDR                        0x05           /* local error, unmatched node id between returned and waiting */
#define HAND_RESP_UNMATCHED_CMD                         0x06           /* local error, unmatched command between returned and waiting */
#define HAND_RESP_DATA_SIZE_TOO_BIG                     0x07           /* local error, size of data to send exceeds the buffer size */
#define HAND_RESP_DATA_INVALID                          0x08           /* local error, data content invalid */
```

- <span style="background-color: #e7f4ffff;">HAND_RESP_HAND_ERROR</span>: 设备错误, 需通过回调获取具体错误码  

- <span style="background-color: #e7f4ffff;">HAND_RESP_SUCCESS</span>: 设备操作成功  

- <span style="background-color: #e7f4ffff;">HAND_RESP_TIMER_FUNC_NOT_SET</span>: 定时器函数未设置, 需调用 HAND_SetTimerFunction ()设置回调函数  

- <span style="background-color: #e7f4ffff;">HAND_RESP_INVALID_CONTEXT</span>: 无效上下文, 上下文为 NULL 或发送函数未设置  

- <span style="background-color: #e7f4ffff;">HAND_RESP_TIMEOUT</span>: 超时错误, 等待节点响应超时  

- <span style="background-color: #e7f4ffff;">HAND_RESP_INVALID_OUT_BUFFER_SIZE</span>: 输出缓冲区大小不匹配  

- <span style="background-color: #e7f4ffff;">HAND_RESP_UNMATCHED_ADDR</span>: 节点地址不匹配  

- <span style="background-color: #e7f4ffff;">HAND_RESP_UNMATCHED_CMD</span>: 命令不匹配  

- <span style="background-color: #e7f4ffff;">HAND_RESP_DATA_SIZE_TOO_BIG</span>: 数据大小超限, 发送数据超过缓冲区大小  

- <span style="background-color: #e7f4ffff;">HAND_RESP_DATA_INVALID</span>: 数据内容无效  

### 自定义命令子命令

用于HAND_SetCustom(), 实现高速读写灵巧手相关控制参数功能  

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

### 创建上下文 <span style="background-color: #e7f4ffff;color: red;">HAND_CreateContext()</span>  

-  方法原型:  
```cpp
void *HAND_CreateContext(
  const void *ctx_private_data,
  HAND_PROTOCOL protocol,
  uint8_t address_master,
  void (*SendDataImpl)(uint8_t addr, uint8_t *data, uint8_t size, void *ctx),
  void (*RecvDataImpl)(void *ctx)
)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx_private_data</code></td>
        <td>上下文私有数据（如串口实例地址）</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>protocol</code></td>
        <td>通信协议（UART 或 I2C）</td>
      </tr>
      <tr>
        <td><code>address_master</code></td>
        <td>主节点地址</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>SendDataImpl</code></td>
        <td>发送数据函数指针</td>
      </tr>
      <tr>
        <td><code>RecvDataImpl</code></td>
        <td>接收数据函数指针</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回上下文指针  
失败: 返回 NULL

- 使用示例
```cpp
void* port = NULL;
void* hand_ctx = NULL;

void* init(const char* port_name, uint32_t baudrate)
{
  // 此处省略串口初始化代码
  return port;
}

void send_data(uint8_t addr, uint8_t* data, uint8_t len, void* hand_ctx)
{
  // 此处省略发数据逻辑
}

void recv_data(void* hand_ctx)
{
  // 此处省略收数据逻辑
}

port = init(port_name, baud_rate);  // 初始化串口
hand_ctx = HAND_CreateContext(port, HAND_PROTOCOL_UART, ADDRESS_MASTER, send_data, recv_data);
```

### 释放上下文指针 <span style="background-color: #e7f4ffff;color: red;">HAND_FreeContext()</span>  

-  方法原型:  
```cpp
void HAND_FreeContext(void *ctx)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
    <tr>
        <td><code>ctx</code></td>
        <td>OHAND上下文指针</td>
      </tr>
    </tbody>
  </table>

- 使用示例
```cpp
HAND_FreeContext(hand_ctx);
```

### 定时器设置<span style="background-color: #e7f4ffff;color: red;">HAND_SetTimerFunction()</span>  

-  方法原型:  
```cpp
void HAND_SetTimerFunction(uint32_t (*GetMilliSecondsImpl)(void), void (*DelayMilliSecondsImpl)(uint32_t ms))
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>GetMilliSecondsImpl</code></td>
        <td>获取毫秒数的函数指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>DelayMilliSecondsImpl</code></td>
        <td>毫秒级延迟函数指针</td>
      </tr>
    </tbody>
  </table>  

- 使用示例  
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

### 获取时间戳<span style="background-color: #e7f4ffff;color: red;">HAND_GetTick()</span>  

- 方法原型:  
```cpp  
uint32_t HAND_GetTick(void)
```

- 使用示例  
```cpp
uint32_t current_tick = HAND_GetTick();
```

### 设置超时时间命令<span style="background-color: #e7f4ffff;color: red;">HAND_SetCommandTimeOut()</span>  

-  方法原型:  
```cpp
void HAND_SetCommandTimeOut(void *ctx, uint16_t timeout)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>timeout</code></td>
        <td>超时时间（毫秒）</td>
      </tr>
    </tbody>
  </table>

- 使用示例  
```cpp
HAND_SetCommandTimeOut(hand_ctx, 255); // 设置超时时间为255毫秒
```

### 数据处理<span style="background-color: #e7f4ffff;color: red;">HAND_OnData()</span>  

-  方法原型:  
```cpp
void HAND_OnData(void *ctx, uint8_t data)
```

- 作用: 将接收到的数据送入内部解析器, 应在接收函数（RecvDataImpl）或中断服务程序（ISR）中调用

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data</code></td>
        <td>接收到的字节数据</td>
      </tr>
    </tbody>
  </table>

- 使用示例  
```cpp
// 假设使用端口为serial
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

### 获取协议版本<span style="background-color: #e7f4ffff;color: red;">HAND_GetProtocolVersion()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetProtocolVersion(void *ctx, uint8_t hand_id, uint8_t *major, uint8_t *minor, uint8_t *remote_err)
``` 

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>major</code></td>
        <td>设备主版本号</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>minor</code></td>
        <td>设备次版本号</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例  
```cpp
uint8_t major_ver, minor_ver;
uint8_t remote_err;
uint8_t used_id = 0x02;
test_err = HAND_GetProtocolVersion(hand_ctx, used_id, &major_ver, &minor_ver, &remote_err);
```

### 获取固件版本<span style="background-color: #e7f4ffff;color: red;">GetFirmwareVersion()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFirmwareVersion(void *ctx, uint8_t hand_id, uint8_t *major, uint8_t *minor, uint16_t *revision, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>major</code></td>
        <td>设备主版本号</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>minor</code></td>
        <td>设备次版本号</td>
      </tr>
      <tr>
        <td><code>revision</code></td>
        <td>设备修订版本号</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例  
```cpp
uint8_t major_ver, minor_ver;
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t revision;
test_err = HAND_GetFirmwareVersion(hand_ctx, used_id, &major_ver, &minor_ver, &revision, &remote_err);
```

### 获取硬件版本<span style="background-color: #e7f4ffff;color: red;">HAND_GetHardwareVersion()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetHardwareVersion(void *ctx, uint8_t hand_id, uint8_t *hw_type, uint8_t *hw_ver, uint16_t *boot_version, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>hw_type</code></td>
        <td>设备硬件类型</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hw_ver</code></td>
        <td>设备硬件版本号</td>
      </tr>
      <tr>
        <td><code>boot_version</code></td>
        <td>设备启动程序版本号</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例  
```cpp
uint8_t hw_type, hw_ver;
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t boot_version;
test_err = HAND_GetHardwareVersion(hand_ctx, used_id, &hw_type, &hw_ver, &boot_version, &remote_err);
```

### 获取矫正数据<span style="background-color: #e7f4ffff;color: red;">HAND_GetCaliData()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetCaliData(void *ctx, uint8_t hand_id, uint16_t *end_pos, uint16_t *start_pos, uint8_t *motor_cnt, uint16_t *thumb_root_pos, uint8_t *thumb_root_pos_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>end_pos</code></td>
        <td>存储终点位置的数组</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>start_pos</code></td>
        <td>存储起点位置的数组</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>thumb_root_pos</code></td>
        <td>拇指根部位置的挡位数组(0, 1, 2)</td>
      </tr>
      <tr>
        <td><code>thumb_root_pos_cnt</code></td>
        <td>拇指根部位置的挡位数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例  
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

### 获取手指PID<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerPID(void *ctx, uint8_t hand_id, uint8_t finger_id, float *p, float *i, float *d, float *g, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>比例系数</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>积分系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>微分系数</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>增益系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例  
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

### 获取手指电流限制值<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerCurrentLimit()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerCurrentLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *current_limit, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_limit</code></td>
        <td>电流限制值</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指电流值<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerCurrent()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerCurrent(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *current, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current</code></td>
        <td>手指电流值</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指目标力值<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerForceTarget()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerForceTarget(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *force_target, uint8_t *remote_err)
```

- 作用: 获取指定手指的目标力值设置，该值用于力控模式下的闭环控制（即设备会自动调节电机输出以维持此目标力）  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force_target</code></td>
        <td>手指目标力值</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指力传感器数据<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerForce()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerForce(void *ctx, uint8_t hand_id, uint8_t finger_id, uint8_t *force_entry_cnt, uint8_t *force, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force_entry_cnt</code></td>
        <td>力数据条目数量</td>
      </tr>
      <tr>
        <td><code>force</code></td>
        <td>存储力数据的变量地址，可存储多点力值，或法向力、切向力及方向</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指绝对位置限制值<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosLimit()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerPosLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *low_limit, uint16_t *high_limit, uint8_t *remote_err)
```

- 作用: 获取指定手指的绝对位置限制范围，用于约束手指的运动区间  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>low_limit</code></td>
        <td>位置下限值</td>
      </tr>
      <tr>
        <td><code>high_limit</code></td>
        <td>位置上限值</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指绝对位置<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosAbs()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerPosAbs(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_pos</code></td>
        <td>目标绝对位置</td>
      </tr>
      <tr>
        <td><code>current_pos</code></td>
        <td>当前绝对位置</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指逻辑位置<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPos()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerPos(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_pos</code></td>
        <td>逻辑目标位置</td>
      </tr>
      <tr>
        <td><code>current_pos</code></td>
        <td>逻辑当前位置</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取手指角度<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerAngle()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerAngle(void *ctx, uint8_t hand_id, uint8_t finger_id, int16_t *target_angle, int16_t *current_angle, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>target_angle</code></td>
        <td>目标角度值, 单位：实际角度×100</td>
      </tr>
      <tr>
        <td><code>current_angle</code></td>
        <td>当前角度值, 单位：实际角度×100</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 获取拇指根部挡位位置<span style="background-color: #e7f4ffff;color: red;">HAND_GetThumbRootPos()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetThumbRootPos(void *ctx, uint8_t hand_id, uint16_t *raw_encoder, uint8_t *pos, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>raw_encoder</code></td>
        <td>指根部原始编码器值, 范围：0~65535</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos</code></td>
        <td>拇指根部映射位置, 范围: 0~2三个挡位</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t raw_encoder;
uint8_t pos;
test_err = HAND_GetThumbRootPos(hand_ctx, used_id, &raw_encoder, &pos, &remote_err);
```

### 获取所有手指绝对位置<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosAbsAll()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerPosAbsAll(void *ctx, uint8_t hand_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *motor_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>target_pos</code></td>
        <td>所有手指目标绝对位置的数组/td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_pos</code></td>
        <td>所有手指当前绝对位置的数组</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
uint16_t raw_target_pos[NUM_MOTORS], raw_current_pos[NUM_MOTORS];
test_err = HAND_GetFingerPosAbsAll(hand_ctx, used_id, raw_target_pos, raw_current_pos, &motor_cnt, &remote_err);
```

### 获取所有手指逻辑位置<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerPosAll()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerPosAll(void *ctx, uint8_t hand_id, uint16_t *target_pos, uint16_t *current_pos, uint8_t *motor_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>target_pos</code></td>
        <td>所有手指目标逻辑位置的数组/td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_pos</code></td>
        <td>所有手指当前逻辑位置的数组</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t raw_target_pos[NUM_MOTORS], raw_current_pos[NUM_MOTORS];
uint8_t motor_cnt = NUM_MOTORS;
test_err = HAND_GetFingerPosAll(hand_ctx, used_id, raw_target_pos, raw_current_pos, &motor_cnt, &remote_err);
```

### 获取所有手指角度<span style="background-color: #e7f4ffff;color: red;">HAND_GetFingerAngleAll()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetFingerAngleAll(void *ctx, uint8_t hand_id, int16_t *target_angle, int16_t *current_angle, uint8_t *motor_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>target_angle</code></td>
        <td>所有手指目标角度值的数组, 单位：实际角度×100/td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_angle</code></td>
        <td>所有手指当前角度值的数组, 单位：实际角度×100</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
int16_t raw_target_angle[NUM_MOTORS], raw_current_angle[NUM_MOTORS];
test_err = HAND_GetFingerAngleAll(hand_ctx, used_id, raw_target_angle, raw_current_angle, &motor_cnt, &remote_err);
```

### 获取自检等级<span style="background-color: #e7f4ffff;color: red;">HAND_GetSelfTestLevel()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetSelfTestLevel(void *ctx, uint8_t hand_id, uint8_t *self_test_level, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>self_test_level</code></td>
        <td>自检等级: 0.不自动自检, 1.自动部分自检, 2.自动全面自检</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t self_test_level;
test_err = HAND_GetSelfTestLevel(hand_ctx, used_id, &self_test_level, &remote_err);
```

### 获取蜂鸣器开关状态<span style="background-color: #e7f4ffff;color: red;">HAND_GetBeepSwitch()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetBeepSwitch(void *ctx, uint8_t hand_id, uint8_t *beep_switch, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>beep_switch</code></td>
        <td>蜂鸣器开关状态: 0.关, 1.开</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint8_t beep_switch;
uint8_t remote_err;
uint8_t used_id = 0x02;
test_err = HAND_GetBeepSwitch(hand_ctx, used_id, &beep_switch, &remote_err);
```

### 获取uid<span style="background-color: #e7f4ffff;color: red;">HAND_GetUID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetUID(void *ctx, uint8_t hand_id, uint32_t *uid_w0, uint32_t *uid_w1, uint32_t *uid_w2, uint8_t *remote_err)
```

- 作用: 获取手部设备的 96 位唯一标识符（UID），用于设备身份识别、唯一性验证等场景

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>uid_w0</code></td>
        <td>设备UID第0个字</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>uid_w1</code></td>
        <td>设备UID第1个字</td>
      </tr>
      <tr>
        <td><code>uid_w0</code></td>
        <td>设备UID第2个字</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint32_t uid_w0, uid_w1, uid_w2;
test_err = HAND_GetUID(hand_ctx, used_id, &uid_w0, &uid_w1, &uid_w2, &test_remote_err);
```

### 获取工厂数据<span style="background-color: #e7f4ffff;color: red;">HAND_GetManufactureData()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetManufactureData(void *ctx, uint8_t hand_id, uint8_t *data, uint8_t *data_size, uint8_t *remote_err)
```

- 作用: 获取手部设备的制造商数据，通常包含设备生产相关的信息（如生产批次、校验信息等）
  
- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>data</code></td>
        <td>制造商数据</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data_size</code></td>
        <td>制造商数据实际长度</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint8_t data_size = 26;
uint8_t* data = (uint8_t*)malloc(data_size * sizeof(uint8_t));
test_err = HAND_GetManufactureData(hand_ctx, used_id, data, &data_size, &test_remote_err);
```

### 获取厂商id<span style="background-color: #e7f4ffff;color: red;">HAND_GetVendorID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetVendorID(void *ctx, uint8_t hand_id, uint16_t *vendor_id, uint8_t *remote_err)
```

- 作用: 获取手部设备的厂商 ID（Vendor ID），用于标识设备的生产厂商，通常为厂商专属的唯一标识符
  
- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>vendor_id</code></td>
        <td>厂商ID</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint16_t vendor_id;
test_err = HAND_GetVendorID(hand_ctx, used_id, &vendor_id, &test_remote_err);
```

### 获取手指力控PID参数<span style="background-color: #e7f4ffff;color: red;">HAND_GetForcePID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetForcePID(void *ctx, uint8_t hand_id, uint8_t finger_id, float *p, float *i, float *d, float *g, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>比例系数</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>积分系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>微分系数</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>增益系数</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
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

### 重启设备<span style="background-color: #e7f4ffff;color: red;">HAND_Reset()</span>  

- 方法原型:  
```cpp
uint8_t HAND_Reset(void *ctx, uint8_t hand_id, uint8_t mode, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>mode</code></td>
        <td>重置模式（0: 启动到用户代码；1：启动到DFU模式）</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t mode = 0;
test_err = HAND_Reset(hand_ctx, used_id, 0, &remote_err);
```

### 设置id<span style="background-color: #e7f4ffff;color: red;">HAND_SetID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetID(void *ctx, uint8_t hand_id, uint8_t new_id, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>new_id</code></td>
        <td>新的设备ID</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 使用示例:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t new_id = 0x03;
test_err = HAND_SetID(hand_ctx, used_id, new_id, &remote_err);
```

### 进入矫正模式<span style="background-color: #e7f4ffff;color: red;">HAND_Calibrate()</span>  

- 方法原型:  
```cpp
uint8_t HAND_Calibrate(void *ctx, uint8_t hand_id, uint16_t key, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>key</code></td>
        <td>矫正密钥</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- **注意: 此功能暂不对外开放, 需要使用此功能时请联系技术支持**

### 获取电池电压<span style="background-color: #e7f4ffff;color: red;">HAND_GetBatteryVoltage()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetBatteryVoltage(void *ctx, uint8_t hand_id, uint16_t *voltage, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>voltage</code></td>
        <td>电池电压</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- **注意: 此功能仅对仿生手有效, 灵巧手无此功能**

### 获取开机次数<span style="background-color: #e7f4ffff;color: red;">HAND_GetUsageStat()</span>  

- 方法原型:  
```cpp
uint8_t HAND_GetUsageStat(void *ctx, uint8_t hand_id, uint32_t *total_use_time, uint32_t *total_open_times, uint8_t motor_cnt, uint8_t *remote_err)
```
- 参数说明:  
    <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>total_use_time</code></td>
        <td>设备的总使用时间</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>total_open_times</code></td>
        <td>各电机的总开机次数</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>
- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- **注意: 此功能仅对仿生手有效, 灵巧手无此功能**

### 关机<span style="background-color: #e7f4ffff;color: red;">HAND_PowerOff()</span>

- 方法原型: 
```cpp
uint8_t HAND_PowerOff(void *ctx, uint8_t hand_id, uint8_t *remote_err)
```  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- **注意: 此功能仅对仿生手有效, 灵巧手无此功能**

### 设置矫正数据<span style="background-color: #e7f4ffff;color: red;">HAND_SetCaliData()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetCaliData(void *ctx, uint8_t hand_id, uint16_t *end_pos, uint16_t *start_pos, uint8_t motor_cnt, uint16_t *thumb_root_pos, uint8_t thumb_root_pos_cnt, uint8_t *remote_err)
```  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>end_pos</code></td>
        <td>各电机的终点位置校准数据</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>start_pos</code></td>
        <td>各电机的起点位置校准数据</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>thumb_root_pos</code></td>
        <td>拇指根部的预设位置校准数据</td>
      </tr>
      <tr>
        <td><code>thumb_root_pos_cnt</code></td>
        <td>拇指根部预设位置的数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码

- **注意: 此功能暂不对外开放, 需要使用此功能时请联系技术支持**

### 设置手指PID参数<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerPID(void *ctx, uint8_t hand_id, uint8_t finger_id, float p, float i, float d, float g, uint8_t *remote_err)
```  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>比例系数</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>积分系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>微分系数</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>增益系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>  

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
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

### 设置手指电流限制值<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerCurrentLimit()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerCurrentLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t current_limit, uint8_t *remote_err)
```  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>current_limit</code></td>
        <td>电流限制值</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>  

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t current_limit_set = 200;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  test_err = HAND_SetFingerCurrentLimit(hand_ctx, used_id, finger_index, current_limit_set, &remote_err);
}
```  

### 设置手指力反馈目标值<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerForceTarget()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerForceTarget(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t force_target, uint8_t *remote_err)
```

- 作用: 设置指定手指的目标力值设置，该值用于力控模式下的闭环控制（即设备会自动调节电机输出以维持此目标力）  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>force_target</code></td>
        <td>目标力值，单位为 mN</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>  

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t force_target_set = 200;
for (int finger_index = 0; finger_index < NUM_FINGERS; finger_index++) {
  test_err = HAND_SetFingerForceTarget(hand_ctx, used_id, finger_index, force_target_set, &remote_err);
}
```

### 设置手指绝对位置限制值<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosLimit()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerPosLimit(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t low_limit, uint16_t high_limit, uint8_t *remote_err)
```  

- 作用: 设置指定手指的绝对位置限制范围，用于约束手指的运动区间  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>low_limit</code></td>
        <td>绝对位置的下限值</td>
      </tr>
      <tr>
        <td><code>high_limit</code></td>
        <td>绝对位置的上限值</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t low_limit_set = 3800, high_limit_set = 16000;
for (int finger_index = 0; finger_index < NUM_MOTORS; finger_index++) {
  test_err = HAND_SetFingerPosLimit(hand_ctx, used_id, finger_index, low_limit_set, high_limit_set, &remote_err);
}
```   

### 启动手指(卡顿时)<span style="background-color: #e7f4ffff;color: red;">HAND_FingerStart()</span>  

- 方法原型:  
```cpp
uint8_t HAND_FingerStart(void *ctx, uint8_t hand_id, uint8_t finger_id_bits, uint8_t *remote_err)
```  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id_bits</code></td>
        <td>手指对应的位掩码</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
const uint8_t finger_ids[NUM_MOTORS] = { 1, 2, 4, 6, 8, 10 };
for (int i = 0; i < NUM_MOTORS; i++) {
  test_err = HAND_FingerStart(hand_ctx, used_id, finger_index, &remote_err);
}

```

### 停止手指<span style="background-color: #e7f4ffff;color: red;">HAND_FingerStop()</span>  

- 方法原型:  
```cpp
uint8_t HAND_FingerStop(void *ctx, uint8_t hand_id, uint8_t finger_id_bits, uint8_t *remote_err)
```  

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id_bits</code></td>
        <td>手指对应的位掩码</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
const uint8_t finger_ids[NUM_MOTORS] = { 1, 2, 4, 6, 8, 10 };
for (int i = 0; i < NUM_MOTORS; i++) {
  test_err = HAND_FingerStop(hand_ctx, used_id, finger_index, &remote_err);
}

```

### 设置手指绝对位置<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosAbs()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerPosAbs(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t raw_pos, uint8_t speed, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>raw_pos</code></td>
        <td>手指的绝对位置</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>运动速度</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
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

### 设置手指逻辑位置<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPos()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerPos(void *ctx, uint8_t hand_id, uint8_t finger_id, uint16_t pos, uint8_t speed, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>pos</code></td>
        <td>目标逻辑位置</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>运动速度</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
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

### 设置手指角度<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerAngle()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerAngle(void *ctx, uint8_t hand_id, uint8_t finger_id, int16_t angle, uint8_t speed, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>angle</code></td>
        <td>目标角度值, 值为实际角度 * 100</td>
      </tr>
      <tr>
        <td><code>speed</code></td>
        <td>运动速度</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
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

### 设置拇指根部位置<span style="background-color: #e7f4ffff;color: red;">HAND_SetThumbRootPos()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetThumbRootPos(void *ctx, uint8_t hand_id, uint8_t pos, uint8_t speed, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>pos</code></td>
        <td>拇指根部的目标位置，只能取 0、1 或 2</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>运动速度</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t speed = 255;
uint8_t pos_set = 1
test_err = HAND_SetThumbRootPos(hand_ctx, used_id, pos_set, speed, &remote_err);
```

### 设置所有手指绝对位置<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosAbsAll()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerPosAbsAll(void *ctx, uint8_t hand_id, uint16_t *raw_pos, uint8_t *speed, uint8_t motor_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>raw_pos</code></td>
        <td>所有手指绝对位置数组</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>所有手指运动速度的数组</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t raw_speed[NUM_MOTORS] = { 100,100,100,100,100,100 };
uint16_t raw_pos_abs[NUM_MOTORS] = { 13000, 13000, 13000, 13000, 13000, 5000 };
uint8_t motor_cnt = NUM_MOTORS;
test_err = HAND_SetFingerPosAbsAll(hand_ctx, used_id, raw_pos_abs, raw_speed, NUM_MOTORS, &remote_err);
```

### 设置所有手指逻辑位置<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerPosAll()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerPosAll(void *ctx, uint8_t hand_id, uint16_t *pos, uint8_t *speed, uint8_t motor_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>pos</code></td>
        <td>所有手指目标逻辑位置的数组</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>所有手指运动速度的数组</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
uint16_t raw_pos[NUM_MOTORS] = { 18000, 33000, 33000, 33000, 33000, 38000 };
test_err = HAND_SetFingerPosAll(hand_ctx, used_id, raw_pos, raw_speed, NUM_MOTORS, &remote_err);
```

### 设置所有手指角度<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerAngleAll()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerAngleAll(void *ctx, uint8_t hand_id, int16_t *angle, uint8_t *speed, uint8_t motor_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>angle</code></td>
        <td>所有手指目标角度的数组</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>speed</code></td>
        <td>所有手指运动速度的数组</td>
      </tr>
      <tr>
        <td><code>motor_cnt</code></td>
        <td>电机数量</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
#define NUM_MOTORS 6
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t motor_cnt = NUM_MOTORS;
int16_t raw_angle[NUM_MOTORS] = { 2000,12000,12000,12000,12000,5000 };
test_err = HAND_SetFingerAngleAll(hand_ctx, used_id, raw_angle, raw_speed, NUM_MOTORS, &remote_err);
```

### 自定义命令,高速读写<span style="background-color: #e7f4ffff;color: red;">HAND_SetCustom()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetCustom(void *ctx, uint8_t hand_id, uint8_t* data, uint8_t send_data_size, uint8_t *recv_data_size, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>data</code></td>
        <td>自定义命令的具体内容数据</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>send_data_size</code></td>
        <td>发送数据的长度</td>
      </tr>
      <tr>
        <td><code>recv_data_size</code></td>
        <td>接收数据的长度</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
详情见此sdk中的示例项目[custom_cmd_test](https://github.com/oymotion/ohand_serial_sdk/tree/master/example/custom_cmd_test){: target="_blank"}

### 设置自检等级<span style="background-color: #e7f4ffff;color: red;">HAND_SetSelfTestLevel()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetSelfTestLevel(void *ctx, uint8_t hand_id, uint8_t self_test_level, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>self_test_level</code></td>
        <td>自检等级, 0: 不自动自检, 1: 部分自检, 2: 完整自检</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t self_test_level_set = 2;
test_err = HAND_SetSelfTestLevel(hand_ctx, used_id, self_test_level_set, &remote_err);
```

### 设置蜂鸣器开关<span style="background-color: #e7f4ffff;color: red;">HAND_SetBeepSwitch()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetBeepSwitch(void *ctx, uint8_t hand_id, uint8_t beep_on, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>beep_on</code></td>
        <td>蜂鸣器开关状态, 0: 关闭, 1: 打开</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint8_t beep_on = 1;
test_err = HAND_SetBeepSwitch(hand_ctx, used_id, beep_on, &remote_err);
```

### 蜂鸣器发声<span style="background-color: #e7f4ffff;color: red;">HAND_Beep()</span>  

- 方法原型:  
```cpp
uint8_t HAND_Beep(void *ctx, uint8_t hand_id, uint16_t duration, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>duration</code></td>
        <td>持续时间, 单位: ms</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
uint16_t duration = 200;
test_err = HAND_Beep(hand_ctx, used_id, duration, &remote_err);
```

### 设置按钮按下次数<span style="background-color: #e7f4ffff;color: red;">HAND_SetButtonPressedCnt()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetButtonPressedCnt(void *ctx, uint8_t hand_id, uint8_t pressed_cnt, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>pressed_cnt</code></td>
        <td>按钮按下的计数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- **注意: 此功能仅对仿生手有效, 灵巧手无此功能**
  
### 触发初始化(条件: 自测模式为0)<span style="background-color: #e7f4ffff;color: red;">HAND_StartInit()</span>  

- 方法原型:  
```cpp
uint8_t HAND_StartInit(void *ctx, uint8_t hand_id, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码    

- 示例代码:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
HAND_SetSelfTestLevel(hand_ctx, used_id, 0, &remote_err);
test_err = HAND_StartInit(hand_ctx, used_id, &remote_err);
```

### 设置工厂数据<span style="background-color: #e7f4ffff;color: red;">HAND_SetManufactureData()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetManufactureData(void *ctx, uint8_t hand_id, uint8_t *data, uint8_t data_size, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>data</code></td>
        <td>制造商数据</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>data_size</code></td>
        <td>制造商数据的大小</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- **注意: 此功能暂不对外开放, 需要使用此功能时请联系技术支持**
  
### 设置手指力控PID参数<span style="background-color: #e7f4ffff;color: red;">HAND_SetFingerForcePID()</span>  

- 方法原型:  
```cpp
uint8_t HAND_SetFingerForcePID(void *ctx, uint8_t hand_id, uint8_t finger_id, float p, float i, float d, float g, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>finger_id</code></td>
        <td>手指id</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>p</code></td>
        <td>比例系数</td>
      </tr>
      <tr>
        <td><code>i</code></td>
        <td>积分系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>d</code></td>
        <td>微分系数</td>
      </tr>
      <tr>
        <td><code>g</code></td>
        <td>增益系数</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>  

- 返回值:  
成功: 返回HAND_RESP_SUCCESS  
失败: 返回相应错误码  

- 示例代码:  
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

### 重置力传感器数据<span style="background-color: #e7f4ffff;color: red;">HAND_ResetForce()</span>  

- 方法原型:  
```cpp
uint8_t HAND_ResetForce(void *ctx, uint8_t hand_id, uint8_t *remote_err)
```

- 参数说明:  
  <table>
    <thead>
      <tr style="background-color: #e6f7ff;">
        <th>参数</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>ctx</code></td>
        <td>OHand 上下文指针</td>
      </tr>
      <tr style="background-color: #e6f7ff;">
        <td><code>hand_id</code></td>
        <td>手部设备id</td>
      </tr>
      <tr>
        <td><code>remote_err</code></td>
        <td>远程错误代码</td>
      </tr>
    </tbody>
  </table>

- 返回值:  
成功: 返回HAND_RESP_SUCCESS    
失败: 返回相应错误码  

- 示例代码:  
```cpp
uint8_t remote_err;
uint8_t used_id = 0x02;
test_err = HAND_ResetForce(hand_ctx, used_id, &remote_err);
```