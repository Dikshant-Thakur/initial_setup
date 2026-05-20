## To install the Gazebo. 
``` apt install -y ros-humble-gazebo-ros-pkgs ``` <br>
and to test it, then run ``` gazebo ```

## To install SLAM & nav2
``` apt update && apt install -y ros-humble-navigation2 ros-humble-nav2-bringup ros-humble-slam-toolbox ```

and to check it ``` ros2 pkg list | grep -E "nav2|slam_toolbox" ``` 

## MiR setup
<!-- Layman terms - To tell the system about ROS app store. 

``` bash
sudo sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

Layman terms -  Donwload and save the ROS App store security password (GPG keys) from the internet. So that our system can trust on ROS softwares. <br>
``` bash
wget http://packages.ros.org/ros.key -O - | sudo apt-key add -
``` -->

apt-get install -y wget curl gnupg2 lsb-release

apt-get update && apt-get install -y python3-vcstool

then 
rosdep init
rosdep update --rosdistro=humble
rosdep install --from-paths src --ignore-src -r -y --rosdistro humble
apt-get update && apt-get install -y python3-colcon-common-extensions



``` Sourcing 
. /usr/share/gazebo/setup.sh
source /opt/ros/humble/setup.bash
source install/setup.bash


