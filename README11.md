- At the end of this section you will know:
- What are ROS2 parameters and when to use them.
- How to declare parameters for your nodes.
- How to get parameters from your node.

<H5>7.5 ROS2 Parameters</H5>

- Configuration parameters and set the values
- no compilation required; just need to change parameters at run-time
- ROS2 parameters are used to set values for nodes at run time
- ROS2 parameters has names and data types- boolean, int, double, string, lists, etc...
<H5>7.6 Declare your parameters </H5>

- ros2 run my_py_pkg number_publisher
- In another terminal, ros2 run my_py_pkg number_counter
- In another terminal, ros2 param (tab twice)
- will list parameter list and we will use list
- ros2 node list
- ros2 param get /number_publisher use_sim_time
- each parameter exits for the node (not global)
- Let see how to declare another parameter
- Go to visual code, in number_publisher.py
- under the constructor "super().__init__("number publisher")"
- add -> self.declare_parameter("test123"), and save the file
- that way we declared a parameter
- then go to ros2_ws folder
- then build - >colcon build --packages-select my_py_pkg --symlink-install
- then we start number_publisher again and when we list parameter -> ros2 param list
- we have test123
- And if we run -> ros2 param get /number_publisher test123
- We will get "parameter not set"
- we can set parameter from ros2 command line tool
- rosd2 run my_py_pkg number_publisher --ros-args -p test123:=3
- and in another terminal if we type -> ros2 param get /number_publisher test123
- you will get the value of the integer
- you can change the value in "ros2 run my_py_pkg number_publisher --ros-arg test123="3.14"
- "ros2 run my_py_pkg number_publisher --ros-arg test123="hello" will output string
- You can add another parameter by
- ros2 run_my_pkg number_publisher --ros-arg -p test123="hello" -p another_param:="Hi"
- and if you want to appear in the list, you need to declear it in number_publisher.py
- self.declear_parameter("another param")
- You can declear any parameter if you want.
- then if we start again and -> ros2 param list
- you will see another param
- ros2 param get /number_publisher another_param
- and with C++, see the tutorial
- We will see how to use the parameter from within your code.

<H5>Get Parameters from a Python Node</H5>

