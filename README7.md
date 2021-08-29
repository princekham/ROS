<H4>40. Debug ROS2 Topics with Command Line Tools</H4>

- run ->ros2 topic (press tab twice to see the commands)
- run -> ros2 run my_py_pkg robot_news_station
- and run ->ros2 topic list (to see the topics)
- run -> ros2 topic info /robot_news (the see the subcribers and publishers
- and the dependency - example_interfaces/msg/String that we will use publisher or subscriber
- we need to send data to robot_news and with example_interfaces/msg/String type
- To create subcriber inside the terminal -> ros2 topic echo /robot_news
- To know the message definition type and what to send to a topic -> ros2 interface show example_interfaces/msg/String
- ros2 topic hz - to get publishing freq of a topic
- ros2 topic bw /robot_news - to see the bandwidth used for the node
- ros2 topic pub -r 10 /robot_news example_interfaces/msg/String "{data:'hello from terminal'}"
- - r 10 - is 10 hz
- ros2 node list -> list the running nodes
- ros2 node info /robot_news_station -> we will get publishers and everything created for this

<H4>Remap a topic at runtime</H4>

- To rename a topic -> ros2 run my_py_pkg robot_news_station --ros-arg -r __node:= my_station -r robot_news:=my_news
- we can rename it and can still use the original node i think


