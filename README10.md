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
- 
