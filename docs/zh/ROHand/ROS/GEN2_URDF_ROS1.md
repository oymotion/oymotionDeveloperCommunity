# ROHAND URDF ROS1包

rohand urdf 包

## 1.克隆

```BASH
cd ~
mkdir -p ros1_ws/src
cd ros1_ws/src
git clone ssh://git@github.com/oymotion/rohand_gen2_urdf_ros1
```

## 2.安装 urdf_parser_py

```BASH
cd ~
pip3 install lxml
git clone https://github.com/ros/urdf_parser_py.git
cd urdf_parser_py
sudo python setup.py install
```

## 3.编译

```BASH
chmod +x rohand_gen2_urdf_ros1/scripts/rohand_joint_state_gui.py
chmod +x rohand_gen2_urdf_ros1/scripts/rohand_urdf.py
cd ~
cd ros1_ws/
catkin_make
source devel/setup.bash
```

## 4.rohand_urdf 节点

| 话题              | 描述                                        |
| ----------------- | ------------------------------------------- |
| "if_slider_joint" | 食指滑块，通过改变食指的位置来控制它         |
| "mf_slider_joint" | 中指滑块，通过改变中指的位置来控制中指       |
| "rf_slider_joint" | 无名指滑块，通过改变无名指的位置来控制它     |
| "lf_slider_joint" | 小指滑块，通过改变小指的位置来控制它         |
| "th_slider_joint" | 大拇指滑块，通过改变拇指的位置来控制它       |
| "th_root_joint"   | 大拇指根部滑块，通过改变其位置来控制拇指根部 |

## 5.运行

启动 'display_r.py or display_l.py' 文件:

左手：

```BASH
roslaunch rohand_gen2_urdf_ros1 display_l.launch
```

右手：

```BASH
roslaunch rohand_gen2_urdf_ros1 display_r.launch
```
