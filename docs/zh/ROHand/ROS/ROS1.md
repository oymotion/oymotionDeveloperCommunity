# 灵巧手ROS1开发包

ROHand的ROS节点，一条总线（即一个端口）需要一个节点。

## 1. 克隆

```BASH
cd ~
mkdir -p ros_ws/src
cd ros_ws/src
git clone ssh://git@github.com/oymotion/rohand_ros_pkg
```

## 2. 准备

安装 pymodbus

```BASH
cd /path/to/workspace  # 切换路径

# 为 Python 创建虚拟环境
virtualenv -p python3 ./venv

# 确保 catkin 不会尝试构建虚拟环境
touch ./venv/CATKIN_IGNORE

# 激活
source ./venv/bin/activate

# 安装 Python 模块
python3 -m pip install pymodbus
```

编辑 ~/.bashrc 文件，并将虚拟环境的库路径添加到 PYTHONPATH 环境变量中

```BASH
export PYTHONPATH=$PYTHONPATH:~/ros_ws/venv/lib/python3.12/site-packages  # 请将 “python3.12” 修改为您实际使用的 Python 版本号
source ~/.bashrc
```

## 3. 编译

```BASH
cd /path/to/workspace
catkin_make
```

## 4. 启动 roscore

```BASH
roscore
```

## 5. 节点 rohand_modbus

ROHand 节点支持 ModBus-RTU 或 ModBus-RTU & SerialCtrl 双协议。请在 OHandSetting 中确认协议类型。  
监听 'target_joint_state' 话题并控制 ROHand，读取当前关节状态并发布到 'current_joint_state'

### 5.1 话题

| 话题                  | 描述                                                                       |
| --------------------- | -------------------------------------------------------------------------- |
| "current_joint_state" | 当前关节状态使用 JointState 消息类型，header 中的 frame_id 用于区分手部 ID |
| "target_joint_state"  | 目标关节状态使用 JointState 消息类型，header 中的 frame_id 用于区分手部 ID |

### 5.2 运行

```BASH
# 打开一个新终端来准备功能包
source /path/to/workspace/devel/bash

# 插入 USB-485 模块至 USB 端口，然后为用户添加访问权限
# 每次插入 USB-485 模块后，请运行以下命令：
sudo chmod o+rw /dev/ttyUSB0  # 将 ttyUSB0 修改为您实际的设备名称

# 请根据您的硬件连接类型，选择对应的命令运行 ROHand 节点
#
# 运行 ROH-A001 节点
rosrun rohand rohand_modbus_a001.py _port_name:=/dev/ttyUSB0 _baudrate:=115200 _hand_ids:=[2] # Modify parameters according to your real case

# 运行 ROH-AP001 节点
rosrun rohand rohand_modbus_ap001.py _port_name:=/dev/ttyUSB0 _baudrate:=115200 _hand_ids:=[2] # Modify parameters according to your real case

# 运行 ROH-LiteS001 节点
rosrun rohand rohand_modbus_lites001.py _port_name:=/dev/ttyUSB0 _baudrate:=115200 _hand_ids:=[2] # Modify parameters according to your real case
```

## 6. 节点 rohand_serial

ROHand 节点仅支持 SerialCtrl 协议，不支持双协议。请在 OHandSetting 中确认协议类型。

功能：监听 'target_joint_state' 话题并控制 ROHand，读取当前关节状态并发布到 'current_joint_state'。

### 6.1 话题

| Topic                 | Description                                                                |
| --------------------- | -------------------------------------------------------------------------- |
| "current_joint_state" | 当前关节状态使用 JointState 消息类型，header 中的 frame_id 用于区分手部 ID |
| "target_joint_state"  | 目标关节状态使用 JointState 消息类型，header 中的 frame_id 用于区分手部 ID |
| "finger_state"        | 手指状态使用 UInt8MultiArray 消息类型                                      |

### 6.2 运行

```BASH
# 打开一个新终端来准备功能包
source /path/to/workspace/devel/bash

# 插入 USB-485 模块至 USB 端口，然后为用户添加访问权限
# 每次插入 USB-485 模块后，请运行以下命令：
sudo chmod o+rw /dev/ttyUSB0  # 将 ttyUSB0 修改为您实际的设备名称

# 请根据您的硬件连接类型，选择对应的命令运行 ROHand 节点
# 运行 ROH-A001 节点
rosrun rohand rohand_serial_a001.py _port_name:=/dev/ttyUSB0 _baudrate:=115200 _hand_ids:=[2] # 请根据您的实际情况修改参数

# 运行 ROH-AP001 节点
rosrun rohand rohand_serial_ap001.py _port_name:=/dev/ttyUSB0 _baudrate:=115200 _hand_ids:=[2] # 请根据您的实际情况修改参数

# 运行 ROH-LiteS001 节点
rosrun rohand rohand_serial_lites001.py _port_name:=/dev/ttyUSB0 _baudrate:=115200 _hand_ids:=[2] # 请根据您的实际情况修改参数
```

手指状态码:

| 状态名称             | Code  | Description  |
| -------------------- | :---: | ------------ |
| STATUS_OPENING       |   0   | 正在展开     |
| STATUS_CLOSING       |   1   | 正在抓取     |
| STATUS_POS_REACHED   |   2   | 位置到位停止 |
| STATUS_OVER_CURRENT  |   3   | 电流保护停止 |
| STATUS_FORCE_REACHED |   4   | 力控到位停止 |
| STATUS_STUCK         |   5   | 电机到位停止 |

## 7. 节点 rohand_teleop

读取按键以修改目标关节角度，然后发布到 'target_joint_state'。

### 7.1 话题

| 话题                 | 描述                                                                       |
| -------------------- | -------------------------------------------------------------------------- |
| "target_joint_state" | 目标关节状态使用 JointState 消息类型，header 中的 frame_id 用于区分手部 ID |

### 7.2 运行

```BASH
# 打开一个新终端来准备功能包
source /path/to/workspace/devel/bash

# 运行节点
rosrun rohand rohand_teleop.py _rohand_teleop_node/target_joint_states:=/rohand_node/target_joint_states _hand_id:=2  # 根据您的实际情况修改参数

# 根据您的类型运行 ROHand 节点
#
# 运行 ROH-A001 节点
rosrun rohand rohand_teleop_a001.py _rohand_teleop_node/target_joint_states:=/rohand_node/target_joint_states _hand_id:=2  # 根据您的实际情况修改参数

# 运行 ROH-AP001 节点
rosrun rohand rohand_teleop_ap001.py _rohand_teleop_node/target_joint_states:=/rohand_node/target_joint_states _hand_id:=2  # 根据您的实际情况修改参数

# 运行 ROH-LiteS001 节点
rosrun rohand rohand_teleop_lites001.py _rohand_teleop_node/target_joint_states:=/rohand_node/target_joint_states _hand_id:=2  # 根据您的实际情况修改参数
```

按以下键位进行操作:

| 按键 | 描述               |
| ---- | ------------------ |
| q    | 退出               |
| a    | 大拇指按步长弯曲   |
| z    | 大拇指按步长放松   |
| s    | 食指按步长弯曲     |
| x    | 食指按步长放松     |
| d    | 中指按步长弯曲     |
| c    | 中指按步长放松     |
| f    | 无名指指按步长弯曲 |
| v    | 无名指按步长放松   |
| g    | 小指按步长弯曲     |
| b    | 小指按步长放松     |
| h    | 大拇指旋转 +步长   |
| n    | 大拇指旋转 -步长   |

步长 = 范围 / 10
