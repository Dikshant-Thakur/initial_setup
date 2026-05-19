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


## To check the container of docker. <br>
``` sudo docker ps -a ``` <br>
After this you will see container ID. Copy that container ID, which you want to run. <br>
And run this line. <br>
``` docker start -ai <container ID> ```
