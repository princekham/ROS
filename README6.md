<H4>36. Write a Python Publisher</H4>

- Go to your package directory -> create a file named "robot_news_station.py"
- And make it executable (to use with similink)

```
cd ros2_ws/src/my_py_pkg/my_py_pkg
touch robot_news_station.py
chmod +x robot_news_station.py
 ```
- copy from python template file and modify it as follow

```
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

from example_interfaces.msg import String


class RobotNewsStationNode(Node):
    def __init__(self):
        super().__init__("robot_news_station")

        self.robot_name_ = "C3PO"
        self.publisher_ = self.create_publisher(String, "robot_news", 10)
        self.timer_ = self.create_timer(0.5, self.publish_news)
        self.get_logger().info("Robot News Station has been started")

    def publish_news(self):
        msg = String()
        msg.data = "Hi, this is " + \
            str(self.robot_name_) + " from the robot news station."
        self.publisher_.publish(msg)


def main(args=None):
    rclpy.init(args=args)
    node = RobotNewsStationNode()
    rclpy.spin(node)
    rclpy.shutdown()


if __name__ == "__main__":
    main()


```
- Node name and the file name can be identical or different
- And add a new line in the setup.py
- "robot_news_station=my_py_pkg.robot_news_station:main"
- where the first robot_news_station is the name of the executable
- And the later is the name of the file followed by where to start : main 
- don't forget to put   <depend>example_interfaces</depend> in the package.xml
- I put it twice and it showed an error :D
- compile it, source ~/.bashrc and run it

<H4>37. Write a Python Publisher</H4>

- creat a file "smartphone.py"
- make it executable
- edit it - use the template

```
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

from example_interfaces.msg import String


class SmartphoneNode(Node):
    def __init__(self):
        super().__init__("smartphone")
        self.subscriber_ = self.create_subscription(
            String, "robot_news", self.callback_robot_news, 10)
        self.get_logger().info("Smartphone has been started.")

    def callback_robot_news(self, msg):
        self.get_logger().info(msg.data)


def main(args=None):
    rclpy.init(args=args)
    node = SmartphoneNode()
    rclpy.spin(node)
    rclpy.shutdown()


if __name__ == "__main__":
    main()

```
- add one line to setup.py
- compile it 
