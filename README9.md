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
  "msg/HardwareStatus.msg"
  )
```
- and compile
- colcon build --packages-select my_robot_interfaces
- Let's see where the messge is installed
- go to my_robot_interfaces folder first -> cd ros2_ws/install/my_robot_interfaces
- Then go to -> cd lib/python3.8/site-packages/my_robot_interfaces/msg
- and ls
- And see what we got in hardware_status.py-> gedit _hardware_status.py
- Go back to my_robot_interfaces folder -> cd ../../../../..
- and go to msg folder -> cd include/my_robot_interfaces/msg/
- and ls
- check what's is inside the hardware_status.hpp -> gedit hardware_status.hpp
- and check what's is inside the hardware_status_struct.hpp
- To see a message definition
- open a terminal ->source .bashrc -> ros2 interface show my_robot_inter (tab)
- and it will show -> ros2 interface show my_robot_interfaces/msg/HardwareStatus
- It will show message definition.
- So to add new msg, you have to add message in msg folder and a new line to CMakeLists.txt
<H5>65. Use Your Custom Message in Python Node</H5>

- First let's go to the python package we created
- cd ros2_ws/src/my_py_pkg/my_py_pkg
- We will create hardware status publisher file so that we can publish this topic on a message
- touch hw_status_publisher.py
- chmod +x hw_status_publisher.py
- Edid the file - use the template ->name it HardwareStatusPublisherNode(Node) ; node = HardwareStatusPublisherNode()
- And node name to -> hardware_status_publisher
- And we will add a mesage type  -> from my_robot_interfaces import HardwareStatus
- Go to settings and add one path-> "~/ros2_ws/install/my_robot_interfaces/lib/python3.8/site-packages/my_robot_interfaces"
- and save the settings
- and we need to add depency for that -> go to package.xml
- and add -> <depend>my_robot_interfaes</depend>
- and we will create a publisher (in hw_status_publisher.py)
- self.hw_status_publisher_=self.create_publisher(HardwareStatus,"hardware_status",10)
- And we will create a timer -> 
```
    self.timer_= self.create_timer(1.0, self.publisher_hw_stutus)
    self.get_logger().info("Hardware status publisher has been started.")
def publish_hw_status(self):
    msg= HardwareStatus()
    msg.termperatuer = 45
    msg.are_mototrs_ready=True
    msg.debug_message ="Nothing special"
    self.hw_status_publisher_.publish(msg)
```
- And add this line to setup.py ->"hw_status_publisher= my_py_pkg.hw_status_publisher:main"
- And we will build -> colcon build --packages-select my_py_pkg --symlink-install
- And in another terminal - source .bashrc
- ros2 run my_py_pkg hw_status_publisher
- And in another terminal
- ros2 topic list; ros2 node list;
-  ros2 topic info /hardware_status
-  ros2 topic echo /hardware_status (will give an error bec we didn't source this terminal here.
-  surce .bashrc then it will work.
-  
