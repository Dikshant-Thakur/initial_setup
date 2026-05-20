## How to setup the docker
**Remove the old version of docker**     <br>
`` sudo apt-get remove docker docker-engine docker.io containerd runc ``. <br>

**Update the system packages**
``` bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release
```
To download the official security from docker and tell Ubuntu trust the source. <br>
``` curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - ```

Again update the system and install the docker.
``` bash    
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

To verify, we have docker or not. <br>
To run the hello world docker. 

``` bash
sudo systemctl status docker 
sudo docker run hello-world     
```
To pull the Ubuntu docker 22.04.   <br>
``` docker pull ubuntu:22.04 ``` <br>
After it runs, then we have to run the docker. <br>
``` docker run -it ubuntu:22.04 /bin/bash ```  <br>
Then we have to tell the X server (security gaurd of graphic card), that give monitor/screen permission to docker container. <br>
``` xhost +local:docker ``` <br>
Here we will launch docker with three arguments - <br>
*--net=host* - Make connection with docker and laptop internet. <br>
*--env="DISPLAY"* - Tells the container where to put the graphics. **Play with another variables**<br>
*--volume=...* - Lets dive deep into this command. <br>
``` bash
--volume="  $HOME/.Xauthority  :  /root/.Xauthority  :  rw  "
  └──1──┘   └───────2───────┘     └───────3──────┘    └─4┘
```
**-v or -volume** is telling the docker that we have to develop the connection/bridge between, host machine and container so that they can share the files. <br>
**$HOME/.Xauthority** - This is the source path, .Xauthority- important file related to GUI. <br>
**/root/.Xauthority** - File path of docker container. <br>
rw - give read and write permissions. 
``` bash 
sudo docker run -it --net=host --env="DISPLAY" -- volume="$HOME/.Xauthority:/root/.Xauthority:rw" ubuntu:22.04 /bin/bash 
```

After it runs, we have to verify the ubuntu and for that. Try this command. <br>
``` cat /etc/os-release ```
## To check the live docker <br>
``` sudo docker ps ```

## To check the container of docker. <br>
``` sudo docker ps -a ``` <br>
After this you will see container ID. Copy that container ID, which you want to run. <br>
And run this line. <br>
``` docker start -ai <container ID> ```

## To see all the images of docker.
``` bash
sudo docker images
```

## To save the container and create an image <br>
While doing this, don't exit from the docker. <br>

``` sudo docker commit <contained_id>:<name> ```

## Check whether the image is saved or not? <br>
``` docker images ```

## Now to run the docker (GUI Version)

``` bash
xhost +local:docker
# This command is to give full NVIDIA power to container
#sudo docker run -it --privileged --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all <docker-image_name> bash
sudo docker run -it --privileged --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all ubuntu22_ros2_gazebo_final_1:nvidia_done bash

# Only limited computational power. NOT RECOMMENDED FOR GAZEBO COOL EXPERIENCE. 
sudo docker run -it --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" <docker-image_name> /bin/bash
```

ubuntu22_ros2_gazebo_final_1:nvidia_done

Then source it ``` source /opt/ros/humble/setup.bash ```. <br>

## To use NVIDIA graphic computation in docker, we need NVIDIA Container Toolkit. 
``` bash
# 1. NVIDIA ka GPG key download karna. Usko system ke trusted keyring me save karna
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
# 2. NVIDIA Container Toolkit repository add karna. Aur us repository ko upar wali GPG key ke saath link karna
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
  sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

#3 Update the Ubunut packages and install NVIDIA container toolkit .
sudo apt-get install -y nvidia-container-toolkit


#4 Configuring docker to use NVIDIA 
sudo nvidia-ctk runtime configure --runtime=docker


#5 Restart the docker
sudo systemctl restart docker

#6 NVIDIA full information
nvidia-smi

```
This command is to give full NVIDIA power to container
``` bash
sudo docker run -it --privileged --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all <docker-image_name> bash
```

``` apt install mesa-utils -y ``` - This package(mesa-utils) has tool - glxinfo, glxgears. <br>
``` glxinfo | grep "OpenGL vendor" ``` ' Layman term - This tells Gazebo which graphic cards. <br>

**How to setup VS code with running container** <br>
Install Dev Container from the extensions. Then Left-Down corner select *><* and then select *Attach to the running container*, make sure your container is running. 



