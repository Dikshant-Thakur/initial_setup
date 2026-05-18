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
After it runs, we have to verify the ubuntu and for that. Try this command. <br>
``` cat /etc/os-release ```