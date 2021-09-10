<H5>8.5 Create and install a launch file</H5>

- we will create a launch file to run two nodes
- cd ros2_ws/src
- ls ; and create a new package; will reduce no of dependency; _bringup is name used for launch file
- ros2 pkg create my_robot_bringup
- cd my_robot_bringup
- ls
- rm -rf include; rm -rf src
- mkdir launch
- ls
- in CMakeLists.txt
- remove
```
# Default to C99
.
.
endif()
```
```
#uncomment the following section in order......
.
.
if (BUILD_TESTING)
.
.
.
endif()
```
- under 
```
#find dependencies
find_package(ament_cmake_REQUIRED)
```
- put these
```
 install (DIRECTORY
    launch
    DESTINATION share/${PROJECT_NAME}
    )
 ```
- which tells
- Now let's create our first launch file
- go to -> ce ros2_ws/src/my_robot_bringup/launch
- touch number_app.launch.py
- chmod +x number_app.launch.py
- let's edit the file
```
from launch import LaunchDescription

def generate_launch_description():
  ld = LaunchDescription()
  
  return ld
  ```
  - before adding scripts, let's build it ; go to a new terminal
  - cd ros2_ws ; colcon build --packages-select my_robot_bringup --symlink-install
  - To launch the launch file, go to another terminal
  - source .bashrc
  - ro2 launch my_robot_bringup number_app.launch.py
  - Now let's add a node to the launch file
  ```
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
  ld = LaunchDescription()
  
  number_publisher_node=Node(
    package="my_py_pkg",
    executable="number_publisher"
    )
    counter_node= Node(
      package="my_cpp_pkg",
      executable ="number_counter"
      )
    ld.add_action(number_publisher_node)
  return ld
  ```
  - we will add dependencies in package.xml
  - after <builtool_depend>amend_cmake........
  ```
  <exec_depend>my_py_pkg</exec_depend>
  <exec_depend>my_cpp_pkg</exec_depend>
  ```
  - now start the launch file again
  - ro2 launch my_robot_bringup number_app.launch.py
<H5>85.Configure your Nodes in a launch file</H5>
  
  - how to  add parameters, how to rename a node, how to remap a topic in a launch file
  - to rename a node -> open number_app.launch.py ->
  - add a new argument under
  ```
  executable = "number_publisher",
  
  ```
  - this
  ```
  name ="my_number_publisher"
  ```
  -And under
  ```
  executable="number_counter",
  ```
  - Add this
  ```
  name="my_number_counter"
  ```
- can launch the launch file again and the node has been renamed.
  - How to remap a topic
  - ros2 topic list (to see the topics)
  - add this to the launch file also like we just did.
  ```
  remapping = [
        ("number", "my_number")
        ]
  ```
  - and
```
  remappings=[
    ("number","my_number"),
    ("number_count","my_number_count")
    ]
```
- save it and lauch the launch file
- rename a service also the same thing
