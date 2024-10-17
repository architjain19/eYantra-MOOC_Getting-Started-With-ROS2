
# Creating a Node in ROS2

> In ROS2, a node is a fundamental building block that encapsulates a specific functionality or process. Each node can communicate with other nodes, either through publish-subscribe or service-client paradigms, enabling modular and scalable software design for robotic applications. Here’s a brief overview of how to create a simple node in ROS2 using Python**




#### 1. Setup the Environment
Ensure you have a ROS 2 workspace ready and sourced.

#### 2. Create a Package, as discribed in previous module.
Follow the ROS 2 package creation steps as outlined in the previous module.


#### 3. Create a Node, In your package directory, create a file named welcome_node.py and add the following code:
Within your package directory, create a file named welcome_node.py with the following content:


```
import rclpy
from rclpy.node import Node

class HelloWorld(Node):
    def __init__(self):
        super().__init__('hello_world')
        self.get_logger().info('Hello World!')

def main(args=None):
    rclpy.init(args=args)
    node = HelloWorld()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

#### Script Breakdown:

-  Importing the Required Libraries

```
import rclpy
from rclpy.node import Node
```
- rclpy: The ROS 2 Python client library that provides all necessary functionality to create and manage nodes, publish messages, subscribe to topics, etc.
- Node: A class from rclpy representing the basic computational unit in ROS 2. 

-  Defining the WelcomeNode Class

```
class WelcomeNode(Node):
    def __init__(self):
        super().__init__('welcome_node')
        self.get_logger().info('Welcome to the package!')
```

- WelcomeNode: A class that inherits from Node, meaning it represents a ROS 2 node.
    - __init__: The constructor initializes the node by giving it a name ('welcome_node') and logs a message: "Welcome to the package!".
    - get_logger(): Provides a logging mechanism to log messages to the ROS 2 logging system.

- The main Function

```
def main(args=None):
    rclpy.init(args=args)
    node = WelcomeNode()
    rclpy.spin_once(node, timeout_sec=1)  # Run the node briefly
    node.destroy_node()
    rclpy.shutdown()
```
1. rclpy.init(): Initializes the ROS 2 system for the node. This step is necessary before creating any nodes or using ROS 2 functionalities.
2. node = WelcomeNode(): Instantiates the WelcomeNode. This means a new ROS 2 node is created, and its initialization process (logging the welcome message) runs.
3. rclpy.spin_once(node, timeout_sec=1): This command allows the node to "spin" (execute any pending tasks like message handling or callbacks) for 1 second. This is a minimal run, as the node doesn't need to subscribe to or publish messages in this script.
4. node.destroy_node(): Destroys the node, freeing up any resources it used.
5. rclpy.shutdown(): Shuts down the ROS 2 system, cleaning up any remaining resources and signaling the end of the program.


#### 4. Update setup.py,Ensure your setup.py includes your script:

In ROS2, adding an entry point in the setup.py file allows you to easily run your node as a command-line tool using the ros2 run command. Here's a detailed explanation of each part of the setup:

The entry_points section allows you to define executable scripts that can be run from the command line. These scripts map to Python functions within your package.

```
entry_points={
    'console_scripts': [
        'hello_world_node = hello_world.hello_world_node:main'
    ],
},
```

- console_scripts: This is the key that tells setuptools to treat these as command-line scripts.

- hello_world.hello_world_node:main: This is the Python path to the function that should be executed when the command is run.

    - hello_world: The name of your package. This should match the package name in setup.py.
    - hello_world_node: The Python file where the main() function is defined.
    - main: The function that is called when you execute the ros2 run command.


#### 5. Build and Run:

Package structure:

```
ros2mooc/
├──src/
   └── hello_world/
       ├── hello_world/
       │   ├── __init__.py
       │   └── hello_world_node.py
       ├── resource/
       ├── test/
       ├── package.xml
       ├── setup.cfg
       └── setup.py
```

Build your package and run the node
```
cd ~/ros2mooc/
colcon build
source install/setup.bash
ros2 run welcome welcome_node
```
Output:
```
[INFO] [1729001664.224730623] [hello_world]: Hello World!
```


#### In Summary 
- This script creates a simple ROS 2 node called WelcomeNode.
- The node logs a welcome message ("Welcome to the package!") when it starts.


**This script forms the foundation for building more complex ROS 2 nodes that can publish/subscribe to topics, provide/use services, and interact with other nodes in a ROS 2 network.**
