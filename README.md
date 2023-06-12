ROS tutorial:
https://docs.ros.org/en/humble/Tutorials.html



# build a package
**building a package should be done in the root of your workspac.**

```sh
cd ~/sofar_ws

colcon build
```

to build just one package
```sh
colcon build --packages-select <package_name>
```
# create a package
for creating package move to the `/src` of your workspac and use the following command:
```sh
ros2 pkg create <package_name> --build-type ament_python --dependencies <dependencies> --node-name <node_name> 
```

**for example:**

```sh
ros2 pkg create turtlesim_controle --build-type ament_python --dependencies rclpy geometry_msgs turtlesim std_msgs --node-name turtle_controle_control
```

after creating the package, you can build it with colcon build command in the root of workspac. 
for example: 
```sh   

cd ~/sofar_ws
 
source install/local_setup.bash
```

**if you don't want to compile the code each time you change it, you can use the following command:** 
```sh
colcon build --packages-select <package_name> --symlink-install
or
colcon build --symlink-instal
```
# launch file
for launch file we should creat a folder and name it launch
then a text file name `<name>.launch.py`

then we should add this lines in setup.py
```sh
import os
from glob import glob
```

and add this line in data_files
```sh
(os.path.join("share",package_name,"launch"), glob("launch/*.launch.py")),
```

# parameters

```sh
ros2 param list /<node name>
ros2 param get <node_name> <parameter_name> 
ros2 param set <node_name> <parameter_name> <value>
```


# service
```sh
ros2 service call <service_name> <service_type> <arguments> [to call a service]
```
----
```sh
ros2 service type <service_name> [to get information about the type of the service]
```
**equivalent to** 
```sh
ros2 service list -t
```
----

    
```sh
ros2 interface show <type_name> [to get the structure of the service]
```

example:
```sh
ros2 service /call /spawn turtlesim/srv/Spawn "{x: 7, y: 4, theta:0.0, name:'turtle2'}"
```

# Aracde
for installing arcade:    `pip3 install arcade`

for test:
```sh
python3
import arcade
arcade.Window(300,199)
```

**Import arcade should be the`first` import in code**

# Custom message and service
Custom messages and services **should be in C++ language**
create a new pacake for Custom message and service:
```sh
ros2 pkg create <name> --build-type ament_cmake --dependencies rclcpp std_msgs
```
create a folder name 'srv' and 'msg'
