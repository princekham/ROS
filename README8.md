<H5>50.Write a Python Service Server</H5>

- Service is define two things - a name and service type
- Here we will use the existing one
- ros2 interface show example_interfaces/src/AddTwoInts- will show the interfaces
- Firt two lines are request and the dashes and then the response
- we will go to ros2 workspace - cd ros2_ws/src/my_py_pkg/my_py_pkg
- And create a file -> touch add_two_ints_server.py
- And make it executable -> chmod +x add_two_ints_server.py
- Edit the file from Visual Studio Code and use the template
- And import the service type -> from example_interfaces_.srv import AddTwoInts
- The new code is as follow:
```
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

from example_interfaces.srv import AddTwoInts


class AddTwoIntsServerNode(Node):
    def __init__(self):
        super().__init__("add_two_ints_server")
        self.server_ = self.create_service(
            AddTwoInts, "add_two_ints", self.callback_add_two_ints)
        self.get_logger().info("Add two ints server has been started.")

    def callback_add_two_ints(self, request, response):
        response.sum = request.a + request.b
        self.get_logger().info(str(request.a) + " + " +
                               str(request.b) + " = " + str(response.sum))
        return response


def main(args=None):
    rclpy.init(args=args)
    node = AddTwoIntsServerNode()
    rclpy.spin(node)
    rclpy.shutdown()


if __name__ == "__main__":
    main()
```
- And go to ROS2_ws and build it -> colcon build --packages-select my_py_pkg 
- And run it with ->ros2 run my_py_pkg add_two_ints_server
- Without client, we can still test the server from the terminal
- ros2 service list -list the services
- ros2 node list - list the running nodes
- ros2 node info /add_two_ints_server - shows the parameters
- ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{a: 3, b: 4}"

<H5>51.Write a Python Service Client</H5>

- we will go to ros2 workspace - cd ros2_ws/src/my_py_pkg/my_py_pkg
- Create a file - touch add_two_ints_client_no_oop.py
- And make it executable -> chmod +x add_two_ints_client_no_oop.py

- The file is as follow
```
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

from example_interfaces.srv import AddTwoInts


def main(args=None):
    rclpy.init(args=args)
    node = Node("add_two_ints_no_oop")

    client = node.create_client(AddTwoInts, "add_two_ints")
    while not client.wait_for_service(1.0):
        node.get_logger().warn("Waiting for Server Add Two Ints...")

    request = AddTwoInts.Request()
    request.a = 3
    request.b = 8

    future = client.call_async(request)
    rclpy.spin_until_future_complete(node, future)

    try:
        response = future.result()
        node.get_logger().info(str(request.a) + " + " +
                               str(request.b) + " = " + str(response.sum))
    except Exception as e:
        node.get_logger().error("Service call failed %r" % (e,))

    rclpy.shutdown()


if __name__ == "__main__":
    main()
```
 - Go to ros2_ws and compile it -> colcon build --packages-select my_py_pkg 
 - And run it ->ros2 run my_py_pkg add_two_ints_client_no_oop
