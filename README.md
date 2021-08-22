# ROS 
image source - https://rosi-images.datasys.swri.edu/
Tutorial link - 
https://industrial-training-master.readthedocs.io/en/melodic/_source/prerequisites/Navigating-the-Ubuntu-GUI.html


Install Ubuntu <br>
Change resolution setting by - <br>
1. sudo apt update
2. sudo apt install build-essential gcc make perl dkms
3. reboot
4. Goto-Device-Insert additional CD
5. Eject CD
6. Restart
7. Do the same process from 4 to 6 again.
8. Then - sudo apt update ; sudo apt upgrade
9. Reboot again
10. Now ready to install ROS 2
11. Install terminator by - sudo apt install terminator
12. Install python3-pip by - sudo apt install python3-pip
13. Install Visual Studio Code by - sudo snap install --classic code
14. ...... Extension - 1. C/C++ for Visual Studion Code 2. CMake for Visual Studio Code 
15. Intall Ros2 Foxy
16. ...... Search "ROS2 Foxy" at google -> choose https://docs.ros.org/en/foxy/Installation.html -> 
17. choose binary package by -> goto Set locale and copy and paste the lines there
18. Copy and paste the followings
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings

18. Then Setup Resources -> copy and pastes lines

sudo apt update && sudo apt install curl gnupg2 lsb-release
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

19. Then update first -> sudo apt update
20. Then Install ROS2 packages -> sudo apt install ros-foxy-desktop
21. - sudo apt install python3-pip
22. - pip3 install -U argcomplete

................................................................
To go to ROS installation folder
- cd /opt/ros/foxy/
- source setup.dash
- ....you have to source to use ROS2 in the terminal .... if not .... cannot use ROS2
- ....in one line -> source /opt/ros/foxy/setup.bash
- .... so to source every time we open terminal -> gedit ~/.bashrc
- Then Reboot
To Test ROS2
- ros2 and enter twice at terminal <br>
- Run -> ros2 run demo_nodes_cpp talker <br>
- And in other terminal -> ros2 run demo_nodes_cpp listener <br>


...................................................................<br>
sudo apt install python3-colcon-common-extensions <br>
.... To use colcon, you have to source it with..... <br>
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash <br>
put in the .bashrc file -> gedit ~/.bashrc<br>

................Creating Workspace...............can name it as you want.............<br>
mkdir ros2_ws <br>
cd ros2_ws/ <br>
mkdir src <br>
colcon build <br>
source local_setup.bash  <br>
... in the gedit .bashrc..... <br>
................Now we will create a package in the src directory.......................<br>
Go to your src directory -> cd ros2_ws/src/
-> ros2 pkg create my_py_pkg --built-tpye ament_python --dependencies rclpy
I am ok with the following line
->ros2 pkg create --build-type ament_python my_py_pkg --dependencies rclpy 

.............Xml has the settings..............

<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>my_py_pkg</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="tgi-lab@todo.todo">tgi-lab</maintainer>
  <license>TODO: License declaration</license>
  
  

  <depend>rclpy</depend>

  <test_depend>ament_copyright</test_depend>
  <test_depend>ament_flake8</test_depend>
  <test_depend>ament_pep257</test_depend>
  <test_depend>python3-pytest</test_depend>

  <export>
    <build_type>ament_python</build_type>
  </export>
</package>
.......................................................
To compile the package 
.......................
go to the package folder -> here ros2_ws
colcon build or to choose one package to build -> colcon build --packages-select my_py_pkg

.............
To create a package in C++
..........................
go to src folder and ->
ros2 pkg create --build-type ament_cmake my_cpp_pkg --dependencies rclcpp
to build package ->colcon build --packages-select my_cpp_pkg

................
To create a node in Python
..................
go to src folder then the workspace

I don't know why I cannot go directly there with one line of code
-> I had to go folder by folder

cd /ros2_ws/src/my_py_pkg/my_py_pkg/

create a file -> touch my_first_node.py
In the visual studio code, open the file and type

#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

def main(args=None):
    rclpy.init(args=args)
    node = Node("py_test")
    node.get_logger().info("Hello ROS2")
    rclpy.spin(node)
    rclpy.shutdown()

if __name__== "__main__":
    main()
    
Then make it exe by

-> chmod +x my_first_node.py
then -> run it -> ./my_first_node.py

Then we will install the node
write this to setpu.py in the console_scripts

"py_node = my_py_pkg.my_first_node:main"

then go to the workspace and run -> colcon build --packages-select my_py_pkg

source .bashrc
ros2 run my_py_pkg py_node

Creating a class in node
The new scripts will be

#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

class MyNode (Node):
    def __init__(self):
      super().__init__("py_test")
      self.get_logger().info("Hello ROS2")

def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    rclpy.shutdown()

if __name__== "__main__":
    main()

........................................
Now let add a timer and a counter
........................................
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

class MyNode (Node):

    def __init__(self):
        super().__init__("py_test")
        self.counter_=0
        self.get_logger().info("Hello ROS2")
        self.create_timer(0.5, self.timer_callback)

    def timer_callback(self):
        self.counter_+=1
        self.get_logger().info("Hello" + str(self.counter_))
def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    rclpy.shutdown()

if __name__== "__main__":
    main()

.................................
Add a node with C++
...............................
- Go to ros2_ws/src/my_cpp_pkg/src$  and create my_first_node.cpp
- edit it in visual studio code as below

#include "rclcpp/rclcpp.hpp"

int main(int argc, char **argv)
{
    rclcpp::init(argc,argv);
    auto node = std::make_shared<rclcpp::Node>("cpp_test");
    RCLCPP_INFO(node->get_logger(),"Hello Cpp Node");
    rclcpp::spin(node);
    rclcpp::shutdown();
    return 0;
}

and change CMakeList.txt file as follow

cmake_minimum_required(VERSION 3.5)
project(my_cpp_pkg)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

add_executable(cpp_node src/my_first_node.cpp)
ament_target_dependencies(cpp_node rclcpp)

install (TARGETS
  cpp_node
  DESTINATION lib/${PROJECT_NAME}
  )

ament_package()

Then build it with 
->colcon build --packages-select my_cpp_pkg
at ros2_ws

ROS2 command line tool for it as follow:

-> source .bashrc
->ros2 run my_cpp_pkg cpp_node 

- 



