<H4>What is a package</H4>
Software in ROS is organized in packages. A package might contain ROS nodes, a ROS-independent library, a dataset, configuration files, a third-party piece of software, or anything else that logically constitutes a useful module. The goal of these packages it to provide this useful functionality in an easy-to-consume manner so that software can be easily reused. In general, ROS packages follow a "Goldilocks" principle: enough functionality to be useful, but not too much that the package is heavyweight and difficult to use from other software.

................Creating Workspace...............can name it as you want.............<br>
mkdir ros2_ws <br>
cd ros2_ws/ <br>
mkdir src <br>
colcon build <br>
source local_setup.bash (I omitted this later in the bashrc)  <br>
instead I put "source ros2_ws/install/setup.bash" and it works <br>
... in the gedit .bashrc..... <br>
<H4>To create a python package in the src directory</H4>
.......................<br>
Go to your src directory -> cd ros2_ws/src/ <br>
-> ros2 pkg create my_py_pkg --built-tpye ament_python --dependencies rclpy<br>
It did not work. I am ok with the following line<br>
->ros2 pkg create --build-type ament_python my_py_pkg --dependencies rclpy <br>

.............Xml has the settings..............<br>
```
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
```
.......................................................



<H4>To compile the python package  </H4>

go to the package folder -> here ros2_ws <br>
colcon build or to choose one package to build like -> colcon build --packages-select my_py_pkg <br>

.......................................
<H4>To create a package in C++</H4>

go to src folder and -> <br>
-> ros2 pkg create --build-type ament_cmake my_cpp_pkg --dependencies rclcpp <br>
to build package ->colcon build --packages-select my_cpp_pkg <br>

........................................
<H4>To create a node in Python </H4>

go to src folder then the workspace <br>

I don't know why I cannot go directly there with one line of code <br>
-> I had to go folder by folder to get to the following folder<br>

cd /ros2_ws/src/my_py_pkg/my_py_pkg/ <br>

create a file -> touch my_first_node.py <br>
In the visual studio code, open the file and type <br>
Note that the name of the node here - "py_test" is not the name of the file <br>
```
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

def main(args=None):
    rclpy.init(args=args)
    node = Node("py_test")
    node.get_logger().info("Hello ROS2")
    rclpy.spin(node) #to continue to be alive; press Ctrl+C to get out of the spin
    rclpy.shutdown()

if __name__== "__main__":
    main()
```  
Then make it exe by

-> chmod +x my_first_node.py <br>
then -> launch it by -> ./my_first_node.py <br>

Then we will install the node to the workspace<br>

write this to setup.py in the console_scripts <br>
("setup.py" file is in the "my_py_pkg" folder) <br>
Those in the "setup.py" file is identical to that in "package.xml"<br>

```
from setuptools import setup

package_name = 'my_py_pkg'

setup(
    name=package_name,
    version='0.0.0',
    packages=[package_name],
    data_files=[
        ('share/ament_index/resource_index/packages',
            ['resource/' + package_name]),
        ('share/' + package_name, ['package.xml']),
    ],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='tgi-lab',
    maintainer_email='tgi-lab@todo.todo',
    description='TODO: Package description',
    license='TODO: License declaration',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            "py_node = my_py_pkg.my_first_node:main"
        ],
    },
)

```

"py_node = my_py_pkg.my_first_node:main" <br>

then go to the workspace and run -> colcon build --packages-select my_py_pkg<br>
To check where the node has been installed -> go to -> cd ros2_ws/install/my_py_pkg/lib/my_py_pkg <br>
The installed package is there <br>
To run it; from that dir -> ./py_node <br>
We won't use those two methods to run a package<br>
Instead, we will use ROS2 command line tool named "ros2 run"<br>
Whenever you run a node always source it to bashrc as follow<br>
source .bashrc
<H5>To run a package </H5>
ros2 run my_py_pkg py_node <br>
meaning -> ros2 run followed by package name and node name <br>
you can start from a new terminal <br>
