## Step 1: Locale (Language aur Character Settings) ##
To install the package name ```local``` to tell the system which language and keyboard characters the system will use. <br>
``` apt update && apt install -y locales ``` <br>

To make the system default language and format settings to English. <br>
``` update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 ``` <br>

Changes the language setting of current  terminal session. <br>
``` export LANG=en_US.UTF-8 ``` <br>


## Step 2: Sources & Repository (ROS 2 ka Address Book Setup)
software-properties-common - It gives the tool to add new tools. curl - Gives the tool to download the files or security key. <br>
``` apt install -y software-properties-common curl ```  <br>
To download the universe repository of ubuntu, where community developed/maintained software like ROS and all. <br>
``` add-apt-repository universe ``` <br>

To download the official ROS2 digital security key and to save locally. <br>
``` bash
curl -sSL [https://raw.githubusercontent.com/ros2/rosdistro/master/ros.key](https://raw.githubusercontent.com/ros2/rosdistro/master/ros.key) -o /usr/share/keyrings/ros-archive-keyring.gpg
 ```

Below line automatically creates *ros2.list* in which it puts the official link of ROS2. And this *$(dpkg --print-architecture)* automatically checks whther PC is intel powered or amd64. <br>
```echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] [http://packages.ros.org/ros2/ubuntu](http://packages.ros.org/ros2/ubuntu) jammy main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null```

## Step 3: Install ROS 2 Packages

Use this command, because on top we add ROS2 link then we have to update again. <br>
``` apt update ``` <br>

To install ROS" humble, colcon tool, python3-argcomplete (wo tab dbakr jis se complete ho jaata hai) <br>
``` apt install -y ros-humble-ros-base python3-colcon-common-extensions python3-argcomplete ``` <br>

## Step 4: Environment Setup
To activate the ROS2. <br>
``` source /opt/ros/humble/setup.bash ```


