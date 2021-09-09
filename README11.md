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

<H5>47. Get Parameters from a Python Node</H5>

- We will use number_publisher.py
- self.declare_parameter("number to publish")
- self.number= self.get_parameter("number_to_publish").value
-  now run -> ros2 run my_py_pkg number_publisher --rors-args -p number_to_publish=4
-  And in another terminal
-  ros2 param get /number_publisher number_to_publish
-  in another terminal
-  ros2 topic echo /number
-  kill the node and start with 5=> ros2 run my_py_pkg number_publisher --rors-args -p number_to_publish=4
-  you will get 5 in another node.
-  If you don't set the parameter, we will get an error.
-  you can add default value -> self.declear_parameter("number_to_publish",2)
-  here 2 is default value
-  we can change the freq of publishing the number by
-  declare another parameter ->self.declare_parameter("publish_frequency",1)
-  we will create a new attribute
-  self.publish_frequency_=self.get_parameter("publisher_frequency").value
-  change the period format by
-  -> self.number_timer = self.create_timer(1.0/self.publish_frequency_, self.publish_number)
-  let's check by running
-  ros2 run my_py_pkg number_publisher --ros-arg -p number_to_publish:=5
-  and we can check the freq by (in a new terminal)-> cd ros2_ws -> ros2 topic hz /number_publisher
-  And started again with 
- -> -  ros2 run my_py_pkg number_publisher --ros-arg -p number_to_publish:=5 -p publish_frequency:=4.5
- and check again with ros2 topic hz /number
- 

