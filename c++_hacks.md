# DATA STRUCTURES
 Represent 3D spcae for a point (location).

``` bash 
const geometry_msgs::msg::Point
 ```
Represents location and rotation of the point (robot). Sophus ek high-end math library hai jo C++ mein use hoti hai, aur SE3d ka matlab hota hai Special Euclidean Group in 3 Dimensions.

```bash
 const Sophus::SE3d &pose 
 ``` 


# LIBRARIES

Math Library
``` bash
#include <cmath> 

```
Data Type Limits Libraries - Taaki hum simit kar ske data type ki value.
``` bash
#include <limits>
```

Input-Output Stream Library.
``` bash
#include <iostream>
```


Algorithms Library. - To compare, to sort , to search etc.

``` bash
#include <algorithm>
```

# Data Structure

Dynamic Array. C++ ki ek smart list hai jiska size automatic chota-bada ho sakta hai.
``` bash
std::vector<double>
```


# Constructor
In python we have a constructor (Jab bhi hamari class ka koi real object (yaani hamara ROS2 node) paida hota hai, toh ek special function automatic chalta hai jo saare variables ko unki shuruati values deta hai. Usi ko constructor kehte hain) jo __init__ mein declare hota hai but in cpp mein ese hota hai <br>
``` bash
PurePursuitComponent::PurePursuitComponent(...)
```
Double colon (::) ke left mein Class ka naam (PurePursuitComponent) hota hai aur right mein Constructor ka naam (PurePursuitComponent). <br>
Aage jaakar hamesha Class ka naam use hota hai, constructor ka naam kahin use nahi hota!. Strict Rule - Dono naam har baari SAME hote hain. <br>

Full line 
``` bash
PurePursuitComponent::PurePursuitComponent(const PurePursuitConfig& config): cfg_(config) {}

#Input for the function
const PurePursuitConfig& config 

# iska mtlb config ki value cfg_ mein daaldo. Same like cfg_ = config but this is but fast.
: cfg_(config) {}



```

