# ROS 
image source - https://rosi-images.datasys.swri.edu/
Tutorial link - 
https://industrial-training-master.readthedocs.io/en/melodic/_source/prerequisites/Navigating-the-Ubuntu-GUI.html


Install Ubuntu
Change resolution setting by -
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
16. ...... Search "ROS2 Foxy" at google -> choose https://docs.ros.org/en/foxy/Installation.html -> choose binary package by -> goto setup local and copy and paste the lines
17. Copy and paste the followings
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
- ros2 and enter twice at terminal
- Run -> ros2 run demo_nodes_cpp talker
- And in other terminal -> ros2 run demo_nodes_cpp listener


...................................................................
sudo apt install python3-colcon-common-extensions
.... To use colcon, you have to source it with.....
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
put in the .bashrc file -> gedit ~/.bashrc

................Creating Workspace...............can name it as you want.............
mkdir ros2_ws
cd ros2_ws/
mkdir src
colcon build
source local_setup.bash 
... in the gedit .bashrc.....
................Now we will create a package in the src directory.......................
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

I don't know why I cannot go directly there with one line of code -> I had to go folder by folder
cd /ros2_ws/src/my_py_pkg/my_py_pkg/






