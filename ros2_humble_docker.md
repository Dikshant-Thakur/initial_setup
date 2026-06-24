## How to setup the ros2-humble in docker


**Update the system packages**
``` bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release
```

**Pull the ros2 humble image**
``` bash
docker pull ros:humble
```

**Then name the container and run it**
``` bash
docker run -it --name my_ros2_container ros:humble
```

**Sourcing**
``` bash
source /opt/ros/humble/setup.bash
```

** Check**
``` bash
ros2 topic list

# should be displayed 
#/parameter_events
#/rosout
```

