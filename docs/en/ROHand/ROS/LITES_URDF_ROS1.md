# ROHAND URDF PACKAGE FOR ROS1

rohand lites urdf package

## 1.Clone

```BASH
cd ~
mkdir -p ros1_ws/src
cd ros1_ws/src
git clone ssh://git@github.com/oymotion/rohand_lites_urdf_ros1
```

## 2.Install urdf_parser_py

```BASH
cd ~
pip3 install lxml
git clone https://github.com/ros/urdf_parser_py.git
cd urdf_parser_py
sudo python setup.py install
```

## 3.Compile

```BASH
chmod +x rohand_lites_urdf_ros1/scripts/rohand_joint_state_gui.py
chmod +x rohand_lites_urdf_ros1/scripts/rohand_urdf.py
cd ~
cd ros1_ws/
catkin_make
source devel/setup.bash
```

## 4.Node rohand_urdf

| Topic             | Description                                                               |
| ----------------- | ------------------------------------------------------------------------- |
| "if_slider_joint" | slider for index finger, control index finger by changing it's position   |
| "mf_slider_joint" | slider for middle finger, control middle finger by changing it's position |
| "rf_slider_joint" | slider for ring finger, control ring finger by changing it's position     |
| "lf_slider_joint" | slider for little finger, control little finger by changing it's position |
| "th_slider_joint" | slider for thumb, control thumb by changing it's position                 |
| "th_root_joint"   | slider for thumb root, control thumb root by changing it's position       |

## 5.RUN

Launch 'display_r.py or display_l.py' file:

Left hand：

```BASH
roslaunch rohand_lites_urdf_ros1 display_l.launch
```

Right hand：

```BASH
roslaunch rohand_lites_urdf_ros1 display_r.launch
```
