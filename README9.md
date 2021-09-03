<H4>Create Custom ROS2 Interfaces</H4>
<H5>64.Create and Build Your First Custom Msg</H5>

- we will create a new package
- go to the scr folder first -> cd ros2_ws/src/
- ros2 pkg create my_robot_interfaces
- go to the my_robot_interfaces package folder -> cd my_robot_interfaces
- and remove the src and include folders - rm -rf include/; rm -rf src/
- and create msg folder ->mkdir msg
- We need to configure - > go to the package.xml ->add three lines after<buildtool_depend>ament_cmake</buildtool_depend>
-  <build_depend>rosidl_default_generators</build_depend>
- <exec_depend>rosidl_default_runtime</exec_depend>
- <member_of_group>rosidl_interface_packages</member_of_group>
- And in the CMakeLists.txt
- find_package(rosidl_default_generators REQUIRED)
- after find_package(ament_cmake REQUIRED)
- And remove the following lines
```
# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()
```
- And the folowing
```
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()
```

- Now your package is ready to build your messages
- Let's create our first message in the msg folder
- go to msg folder -> cd msg/
- create a new file -> touch HardwareStatus.msg (must be Uppercase now underscore, no msg in the name)
- put the followings in the file
```
int64 temperature
bool are_motors_ready
string debug_message
```
- and save it.
- Go to the CMakeLists add the followings
```
rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/HarewareStatus.msg"
```
- and compile
- colcon build --packages-select my_robot_interfaces
