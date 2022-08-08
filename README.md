# TurtleBot3 SLAM
In this repository I will show the steps of using TurtleBot3 SLAM Simulation.
In TurtleBot3 they provide three Gazebo environments Empty World, TurtleBot3 World and TurtleBot3 House but for the SLAM simulation you can use the last two.

They look as follow:
### Empty World
<img src="https://user-images.githubusercontent.com/108296165/183515339-d80c3998-fa56-49c5-a041-5b9e08bed9ad.png" width="600" height="400">

### TurtleBot3 World
<img src="https://user-images.githubusercontent.com/108296165/183515504-be5bcd54-cacb-4778-a34d-83120d178f61.png" width="600" height="400">

### TurtleBot3 House
<img src="https://user-images.githubusercontent.com/108296165/183515623-1837e181-3f93-4cf6-a693-effc173a1e7c.png" width="600" height="400">

In this tutorial i will use the TurtleBot3 World.

## Setup
This command is for ROS neotic, first in the triminal use the following commands:
```
$ sudo apt update
$ sudo apt upgrade
$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_noetic.sh
$ chmod 755 ./install_ros_noetic.sh 
$ bash ./install_ros_noetic.sh
```

### Install Dependent ROS Packages
```
$ sudo apt-get install ros-noetic-joy ros-noetic-teleop-twist-joy \
  ros-noetic-teleop-twist-keyboard ros-noetic-laser-proc \
  ros-noetic-rgbd-launch ros-noetic-rosserial-arduino \
  ros-noetic-rosserial-python ros-noetic-rosserial-client \
  ros-noetic-rosserial-msgs ros-noetic-amcl ros-noetic-map-server \
  ros-noetic-move-base ros-noetic-urdf ros-noetic-xacro \
  ros-noetic-compressed-image-transport ros-noetic-rqt* ros-noetic-rviz \
  ros-noetic-gmapping ros-noetic-navigation ros-noetic-interactive-markers
  ```
### Install TurtleBot3 Packages
```
$ sudo apt install ros-noetic-dynamixel-sdk
$ sudo apt install ros-noetic-turtlebot3-msgs
$ sudo apt install ros-noetic-turtlebot3
```

## Gazebo Simulation
### Install The Simulation Package
```
$ cd ~/catkin_ws/src/
$ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make
```
### Launch Simulation World
As we saw before there is three Gazebo environments.
### 1.Empty world 
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```
there is three TURTLEBOT3_MODEL: burger, waffle and waffle_pi

### 2.TurtleBot3 World
```
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

### 3.TurtleBot3 House
```
$ export TURTLEBOT3_MODEL=waffle_pi
$ roslaunch turtlebot3_gazebo turtlebot3_house.launch
```

## SLAM Simulation
SLAM in gazebo simulation is similar to actual TurtleBot3 SLAM.
### Launch Simulation World
you can run it using the the last two enviroments, and for the TURTLEBOT3_MODEL you can choose any of the three models.
I choose world enviroment and burger model.
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
This will show the following:

<img src="https://user-images.githubusercontent.com/108296165/183520698-dd6386f7-9508-4ae7-aea5-392c9474457b.png" width="600" height="400">
### Run SLAM Node
open a new terminal, and type the following commands.
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
This will show the following:

<img src="https://user-images.githubusercontent.com/108296165/183521855-d3c3eabe-3401-4002-8ed2-0451bd81a619.png" width="600" height="400">

## Run Teleoperation Node
also here open a new terminal, and type the following commands. 

```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
<img src="https://user-images.githubusercontent.com/108296165/183522291-d138d404-402a-405c-87d5-66db1167926c.png" width="600" height="400">

Then you can type the showed command to move the robot around in the simulator, so you can can draw the full map of the place, and after finshing it the result will be as follow:

<img src="https://user-images.githubusercontent.com/108296165/183522662-9c035c61-be78-4948-871d-c840e95f9a50.png" width="600" height="400">

## Save Map
you can save the map using the following commands:
```
$ rosrun map_server map_saver -f ~/map
```
it can be saved as following:

<img src="https://user-images.githubusercontent.com/108296165/183522957-8dd2790b-68b7-4609-a53a-91188edf85a1.png" width="600" height="400">





