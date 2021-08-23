

<H5>Creating a class in node </H5>
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
