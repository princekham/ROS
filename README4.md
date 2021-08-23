<H4>26. Debug and Monitor Your Nodes with ros2 cli</H4>
<H5>ROS2 commands</H5>

- source /opt/ros/foxy/setup.bash
- source ~/ros2_ws/install/setup.bash
- source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
- Make sure you have the above two lines in ~/.bashrc 
- Or you can source directly -> source ~/.bashrc 

To see the ROS2 command ->ros2 (and press tab button twice)<br>
In the command <br>
ros2 run demo_nodes_cpp talker <br>
the package name is demo_nodes_cpp and the executable is talker <br>
If you want to see all the executables of a package, press tab twice after the package name<br>
use - h suffix for help <br>
- ros2 node (for viewing all the nodes)
- ros2 node list (for viewing the running nodes)
- ros2 node info /py_test (will give information about the node)
- we should not have a node with the same name on the graph

<H4>27. Rename a node at runtime</H4>
- $ ros2 run my_pypkg py_node --ros-args --remap __node:=abc (here  abc is a new name)






