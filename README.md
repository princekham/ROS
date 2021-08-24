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
.... To use colcon autocompletion, you have to source it with..... <br>
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash <br>
put in the .bashrc file -> gedit ~/.bashrc<br>



