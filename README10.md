<H5>67. Create and Build Your First Custom srv</H5>

- Go to my_robot_interfaces folder -> cd ros2_ws/my_robot_interfaces/
- ls
- create a directory -> mkdir srv
- go to that folder -> cd srv
- create a file -> touch ComputeRectangle.srv
- go to the file -> 
```
float64 length
float64 width
---
float64 area
```

- in package.xml make sure you have these three lines
```
<build_depend>
<exec_depend>
<member_of_group>
````
And in CMakeLists.txt, make sure you have
```
find package(rosidl_default_generators REQUIRED)
```
AND add a new line at the bottom
```
"srv/ComputeRectangleArea.srv"

```
- Now go to ros2_ws folder and build it -> colcon build --packages -select my_robot_interfaces
- and in another terminal -> source and run
- > source .bashrc ; -> ros2 interfaces show my_robot_interfaces/
- > ros2 interface show my_robot_interfaces/src/ComputeRectangleArea
<H5> Debug Msg and Srv with ROS2 tools</H5>

- source .bashrc
- ros2 interface (tab twice) will show the interface command
- ros2 interface show my_robot_interfaces/srv/ComputeRectangleArea (This will show in inputs and outputs)
- ros2 interface show example_interfaces/msg/String
- (So the above two commands show the srv and msg) type
- ros2 interface list (list every installed or built)- msg and srv (will show the srv and msg you can use)
- ros2 interface package sensor_msg (to get more specific on sensor_msg)
- In another terminal, first have to run -> source .bashrc ->then run
- ros2 run my_py_pk hw_status_publisher
- And In another terminal, source .bashrc ; see the running node ->ros2 node list
- See the info ->ros2 node info /harware_status_publisher (from the node you can see the topics and the name of the interface ...)
- can also find it by -> ros2 topic list (you will get a list)
- and from that list, for more info -> ros2 topic info /hardware_status
- from that you will get ther name of the interface and from that
- ros2 interface show my_robot_interfaces/msg/HardwareStatus (you can find what you need to send or receive)
- now we will kill the process and run the service server -> ros2 run my_py_pkg add_two_ints_server
- Here we will do the same thing
- ->ros2 node list ->ros2 node info /add_two_ints_server
- you will see the name of the interface and msg
- ros2 service list (will show the interfaces)
- ros2 service type /add_two_ints
- ros2 interface show example_interfaces/srv/AddTwoInts (you will get the interfaces)
- Make sure to make a difference between topic (communicaiton layer) and interfaces (what you send )
- Same for Service (communication layer) and interfaces is (what you req and get responses)
