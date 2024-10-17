## Messages: Data Packets Exchanged Between Nodes


> Messages are the data structures used to exchange information between ROS nodes over topics. Each message has a specific type, which defines the data it can carry. ROS provides a variety of predefined message types for common use cases (such as images, velocity commands, and sensor readings), and users can define custom message types as needed.


#### Key Characteristics of Messages:
> - Typed Data Structures: Every message in ROS has a predefined structure (e.g., a set of fields), which defines the kind of data it can hold.
> - Modularity and Extensibility: Messages are modular, allowing nodes to exchange only the necessary data. ROS provides standard messages for common robotics tasks, and users can extend these by creating custom messages.


#### std_msgs
stands for Standard Messages and is one of the most basic message packages provided by ROS. It contains common message types that are used for communication between nodes across various applications. These message types are simple and fundamental, meant to cover a wide range of basic use cases.

#### Common Message Types in std_msgs:
> - std_msgs/String
> - std_msgs/Int32
> - std_msgs/Float64
> - std_msgs/Bool

For more detailed information, including specific message types, visit the ROS 2 Humble [Standard Messages](https://docs.ros.org/en/humble/p/std_msgs/) documentation.

For [Creating custom msg and srv files](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Custom-ROS2-Interfaces.html)