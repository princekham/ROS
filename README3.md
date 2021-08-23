

<H4>Creating a class in node </H4>
The new scripts will be <br>

```
#!/usr/bin/env python3 <br>
import rclpy <br>
from rclpy.node import Node <br>

class MyNode (Node): <br>
    def __init__(self):<br>
      super().__init__("py_test")<br>
      self.get_logger().info("Hello ROS2")<br>

def main(args=None):<br>
    rclpy.init(args=args)<br>
    node = MyNode()<br>
    rclpy.spin(node)<br>
    rclpy.shutdown()<br>

if __name__== "__main__":<br>
    main()<br>
    
````

to compile is the same process as above <br>

<H5>Now let add a timer and a counter</H5>

```
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
```

to compile is the same process as above <br>


<H5>Add a node with C++</H5>

- Go to ros2_ws/src/my_cpp_pkg/src$  and create my_first_node.cpp <br>
- edit it in visual studio code as below <br>
```
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
```
and change CMakeList.txt file as follow to compile and install the package <br>
some of the CMakeList.txt file are truncated <br>
```
cmake_minimum_required(VERSION 3.5) 
project(my_cpp_pkg) 

##Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

##find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

add_executable(cpp_node src/my_first_node.cpp) // This is what added to the file
ament_target_dependencies(cpp_node rclcpp) // This is what added to the file
// Those are added too
install (TARGETS
  cpp_node
  DESTINATION lib/${PROJECT_NAME}
  )
// till here
ament_package()
```
What is added to the file are commented <br>
Those two lines will actually create executables<br>

Then build it with <br>
->colcon build --packages-select my_cpp_pkg <br>
at ros2_ws <br>
Run it with -> ./cpp_node <br>
But now you don't always need to the base folder because you have installed it<br>

We can use ROS2 command line tool as follow: <br>

-> source .bashrc <br>
->ros2 run my_cpp_pkg cpp_node <br>

- 

