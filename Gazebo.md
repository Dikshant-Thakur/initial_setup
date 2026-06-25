# How to insert your models into gazebo model
Step 1: Model Folder Structure Banayein <br>
In your directory, go to ~/.gazebo/models/, the structure should be like this otherwise create the structure like this. <br>
```text
my_model/
├── model.config
├── model.sdf
└── meshes/
    ├── tunnel_info.dae
    └── tunnel_road_texture_baseColor.jpeg
``` 

Step 2: model.config File Banayein <br>
my_model folder ke andar ek khali text file banayein, uska naam rakhein model.config aur uske andar yeh code copy-paste kar dein:

``` bash
<?xml version="1.0"?>
<model>
  <name>My Model</name>
  <version>1.0</version>
  <sdf version="1.6">model.sdf</sdf>
  <author>
    <name>Your Name</name>
    <email>your@email.com</email>
  </author>
  <description>
    Write your description here.
  </description>
</model>
```

Step 3: model.sdf File Banayein. static or not, it depends. <br>
``` bash
<?xml version="1.0" ?>
<sdf version="1.6">
  <model name="model">
    <static>true</static>
    <link name="link">
      <collision name="collision">
        <geometry>
          <mesh>
            <uri>model://model/meshes/model.dae</uri>
          </mesh>
        </geometry>
      </collision>
      <visual name="visual">
        <geometry>
          <mesh>
            <uri>model://model/meshes/model.dae</uri>
          </mesh>
        </geometry>
      </visual>
    </link>
  </model>
</static>
```

Step 4: Folder ko Gazebo Directory mein Daalein <br>
Ab is poore my_tunnel folder ko uthakar Gazebo ke default model directory mein copy kar dein: <br>
Linux par path hota hai: /home/YOUR_USERNAME/.gazebo/models/
(Aap apne terminal mein cp -r model ~/.gazebo/models/ chala sakte hain. Agar .gazebo folder na dikhe toh Ctrl + H dabayein hidden folders dekhne ke liye).