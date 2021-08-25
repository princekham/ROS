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
#include "rclcpp/rclcpp.hpp"
#include "example_interfaces/msg/string.hpp"

class RobotNewsStationNode : public rclcpp::Node
{
public:
    RobotNewsStationNode() : Node("robot_news_station"), robot_name_("R2D2")
    {
        publisher_ = this->create_publisher<example_interfaces::msg::String>("robot_news", 10);
        timer_ = this->create_wall_timer(std::chrono::milliseconds(500),
                                         std::bind(&RobotNewsStationNode::publishNews, this));
        RCLCPP_INFO(this->get_logger(), "Robot News Station has been started.");
    }

private:
    void publishNews()
    {
        auto msg = example_interfaces::msg::String();
        msg.data = std::string("Hi, this is ") + robot_name_ + std::string(" from the Robot News Station");
        publisher_->publish(msg);
    }

    std::string robot_name_;
    rclcpp::Publisher<example_interfaces::msg::String>::SharedPtr publisher_;
    rclcpp::TimerBase::SharedPtr timer_;
};

int main(int argc, char **argv)
{
    rclcpp::init(argc, argv);
    auto node = std::make_shared<RobotNewsStationNode>();
    rclcpp::spin(node);
    rclcpp::shutdown();
    return 0;
}

```
- Node name and the file name can be identical or different
- And add a new line in the setup.py
- "robot_news_station=my_py_pkg.robot_news_station"
- where the first robot_news_station is the name of the executable
- And the later is the name of the file followed by where to start : main
- 
- don't forget to put   <depend>example_interfaces</depend> in the package.xml
- I put it twice and it showed an error :D
- compile it, source ~/.bashrc and run it



