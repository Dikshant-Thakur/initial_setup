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

# Proceudre to use the docker. 
### Run the docker
``` bash
# Run the docker
sudo docker run -it --privileged --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all dikki69/ros2_info_final bash
```
what happens - docker run ne Docker Engine se kaha: "Bhai, is image ke blueprint ko use karke ek ekdum brand new, alag se isolated kamra (Container) taiyaar karo." Is command ke andar jo baki flags hain (--privileged, --net=host, --gpus all, DISPLAY), unhone us naye kamre ke sath kuch pipelines (connections) permanent jod diye—jaise tumhare laptop ka graphics card, internet, aur laptop ki screen. Aur aakhiri shabd bash ne tumhein us kamre ka terminal de diya. <br
Tumne us naye container ke andar files modify karein, Blender dale, sab badlav kiye. Yeh saare badlav us naye container ki layer mein save ho gaye.

### Exit the container
``` bash
exit
```
What happens - Jaise hi tumne exit dabaya, tum container ke terminal se baahar apne laptop ke normal terminal par aa gaye. Woh container abhi bhi tumhare laptop ki hard disk par maujood hai. Woh container ab chal nahi raha hai, woh Sleep/Freeze mode mein chala gaya hai. Jo badlav tumne kiye the (modified files, blender), woh sab us container ke andar freeze ho chuke hain, kuch bhi delete nahi hua hai. <br>
**One more thing to note** - stop command belongs to docker and exit command belongs to linuex. Interactive session is differnet, exit runs in the docker terminal and stop command runs in the hoest terminal but result is same. 

### How to reopen that container
Ab tum agle din aaye, laptop chalu kiya, aur tumhein usi container par wapas kaam karna hai. Ab tumhein lambi command nahi chalani (kyunki run chalane se naya khaali container ban jayega). Ab tum yeh basic steps follow karoge:
``` bash
# Step A: Kaise check karein ki hamara container kahan hai?
sudo docker ps -a
#-a ka matlab hai "All" (chahe chal rahe hon ya so rahe hon, saare dikhao).
```
Tumhein list mein tumhara container dikhega. Uska status Exited hoga. Wahan se uski CONTAINER ID (jaise d73f2694e98e) ya uska NAME dekh lo. 
``` bash
#Step B: Host par screen ki permission do
xhost +local:root
```
Kyunki laptop restart hone par GUI permissions reset ho jati hain, isliye pehle laptop ki screen ka rasta kholo.

``` bash
# Step C: Us soye hue container ko chalu karo
sudo docker start <CONTAINER_ID_YA_NAME>
```
Ab us purane container ko jagane ke liye (docker run ki jagah) bas start chalao. Isse kya hua? Tumhara wahi container background mein wapas zinda (Up status) ho gaya, aur uski purani saari responsibilities (NVIDIA driver, ports) jo pehli baar run karne par jodi thi, woh dobara active ho gayi.

``` bash
# Step D: Uske andar enter karo
sudo docker exec -it <CONTAINER_ID_YA_NAME> bash

```
Ab container chal raha hai, uske andar ghusne ke liye chalao. Boom! Aap wapas usi container ke terminal ke andar ho. Wahan ls karke dekhoge toh tumhari pichli modified files bhi milengi,


## To see all the images of docker.
``` bash
sudo docker images
```
## To check the live docker <br>
``` bash
sudo docker ps 
```

## To check the container of docker. <br>
``` bash 
sudo docker ps -a 

# After this you will see container ID. Copy that container ID, which you want to run. 
# And run this line. 

docker start -ai <container ID> 
``` 


## To save the container and create an image <br>
While doing this, don't exit from the docker. <br>

``` bash
sudo docker commit <contained_id> <name> 


docker images 

 ```

## To stop the container 
``` bash docker stop <container_id> ```

## To delete the image of the docker
``` bash
sudo docker rmi <IMAGE_ID_YA_NAME>
```
Docker bohot samajhdar hai. Agar us image se bana hua koi bhi container (chahe woh stop state mein hi kyun na ho) tumhare system mein maujood hai, toh Docker us image ko delete nahi karne dega. Woh kahega ki pehle uske bachon (containers) ko saaf karo! <br>
Agar aisa error aaye, toh yeh do kaam karne padenge: <br>

Step 1 - Pehle sudo docker ps -a karke dekh lo ki us image ka kaunsa container pada hai. Fir use delete karo:
``` bash
sudo docker rm <CONTAINER_ID_YA_NAME>
#(Yahan rm use hoga kyunki hum container mita rahe hain).
```
Step 2 - Ab Image ko delete karo. Jab us image se jude saare containers delete ho jayein, tab wapas chalao.
``` bash
sudo docker rmi <IMAGE_ID>
```



## Now to run the docker (GUI Version)

``` bash
xhost +local:docker
# This command is to give full NVIDIA power to container
#sudo docker run -it --privileged --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all <docker-image_name> bash
sudo docker run -it --privileged --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all kiss_icp_setup_done:latest bash

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
``` glxinfo | grep "OpenGL vendor" ``` ' Layman term - This tells Gazebo which graphic card, Gazebo is using. <br>

**How to setup VS code with running container** <br>
Install Dev Container from the extensions. Then Left-Down corner select **><** and then select *Attach to the running container*, make sure your container is running. 

## To check the size of docker
``` bash
sudo docker system df 
``` 

In detail <br>

``` bash
sudo docker system df -v

```

## How to download the docker image

1. Docker Hub image ko Download (Pull) karein
``` bash
docker pull <image_name>
```
then check the docker image and enjoy!.


## How to download blender in the docker image.

``` bash
apt update
```

``` bash
apt install -y software-properties-common sudo
```

``` bash
apt install -y blender
```

## How to copy file from host to docker
``` bash
docker cp /path/to/your/host/model.zip <container_name_or_id>:/root/
```