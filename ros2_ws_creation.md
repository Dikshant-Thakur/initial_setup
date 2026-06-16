# CREATION OF ROS2 PACKAGE
## Option 1: Agar C++ (CMake) package banana hai
C++ mein nodes likhne wale ho, toh terminal mein apne src folder ke andar jao aur yeh command chalao:
``` bash
ros2 pkg create --build-type ament_cmake <package_name>
```
## Option 2: Agar Python package banana hai
Agar tum Python mein scripts likhne wale ho, toh src folder ke andar yeh command chalao:
``` bash
ros2 pkg create --build-type ament_python <package_name>
```

## Package Banane ke Baad ka Step (Crucial)
``` bash
colcon build --packages-select <package_name>
source install/setup.bash
```
