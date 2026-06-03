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

OR IF THE ABOVE COMMAND OF UNIVERSE NOT WORKING. TRY TO DOWNLOAD THE OFFICIAL GPG KEY DIRECT FROM UBUNTU.
``` bash
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F42ED6FBAB17C654
```

Below line automatically creates *ros2.list* in which it puts the official link of ROS2. And this *$(dpkg --print-architecture)* automatically checks whther PC is intel powered or amd64. <br>
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] [http://packages.ros.org/ros2/ubuntu](http://packages.ros.org/ros2/ubuntu) jammy main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

## Step 3: Install ROS 2 Packages

Use this command, because on top we add ROS2 link then we have to update again. <br>
``` apt update ``` <br>

To install ROS" humble <br>
``` apt install -y ros-humble-desktop ``` <br>

## Step 4: Environment Setup and check
To activate the ROS2. <br>
``` source /opt/ros/humble/setup.bash ``` <br>
To check the GUI version of it. <br>
``` rviz2 ```  


# Commands on ROS-2

``` rosdep install --from-paths src --ignore-src -r -y ``` <br>
rosdep ek tool hai jo ROS packages ki required system dependencies install karta hai. <br>
``` --from-paths src ``` - src folder ke andar jitne ROS packages hain, unko scan karo. <br>
``` --ignore-src ``` - Jo packages source code ke form me already src me present hain, unko install mat karo. Sirf missing external dependencies install karo. <br>
``` -r = recursive / continue on error ``` - Agar kisi ek dependency me error aaye, toh command completely stop nahi hogi. Baaki packages pe continue karegi.


