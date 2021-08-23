<H4>To compile the package  </H4>

go to the package folder -> here ros2_ws <br>
colcon build or to choose one package to build like -> colcon build --packages-select my_py_pkg <br>

.............
<H4>To create a package in C++<H4>
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

