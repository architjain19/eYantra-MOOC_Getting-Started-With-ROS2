# Key Concepts of ROS 2 Nodes
 
**In ROS 2, nodes are the fundamental building blocks of the system, much like in ROS 1. They enable the creation of modular and reusable software components that perform specific tasks. However, ROS 2 introduces several improvements and changes in the API and architecture to enhance performance, reliability, and scalability. Here are the key concepts:**

### Node Initialization:

- Every node must initialize itself and provide a unique name. This is done using the rclpy or rclcpp libraries for Python and C++ respectively.


- 1. Importing Required Modules:

```bash
import rclpy
from rclpy.node import Node
```
- rclpy: The main library for ROS 2 in Python. It provides the necessary tools and functions to create and manage nodes.

- rclpy.node.Node: The base class for creating nodes in ROS 2. It provides all the necessary methods and properties to interact with the ROS 2 ecosystem.


- 2. Defining the Node Class:

```bash
class MyNode(Node):
    def __init__(self):
        super().__init__('node_name')
```


- class MyNode(Node): This line defines a new class MyNode that inherits from Node, which means MyNode has all the properties and methods of a ROS 2 node.
- def __init__(self): The constructor method for the class MyNode.
- super().__init__('node_name'): This calls the constructor of the parent class Node and initializes the node with the name 'node_name'. This name uniquely identifies the node within the ROS 2 graph.


- 3. Main Function:

```bash
def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()
```


- def main(args=None): Defines the main function which is the entry point of the program.
- rclpy.init(args=args): Initializes the ROS 2 communication infrastructure. This must be called before any ROS 2 nodes are created.
- node = MyNode(): Creates an instance of the MyNode class, effectively initializing your custom node.
- rclpy.spin(node): Keeps the node running, allowing it to process callbacks and interact with the ROS 2 system. This function blocks until the node is shut down.
- node.destroy_node(): Properly destroys the node to clean up any resources used.
- rclpy.shutdown(): Shuts down the ROS 2 communication infrastructure. This should be called after all nodes have been destroyed.

### Entry Point:

```bash
if __name__ == '__main__':
    main()
```
This is a standard Python idiom to ensure that the main function is called only when the script is executed directly, not when it is imported as a module in another script.

```bash
import rclpy
from rclpy.node import Node

class MyNode(Node):
    def __init__(self):
        super().__init__('node_name')

def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```
**This script forms the foundation for building more complex ROS 2 nodes that can publish/subscribe to topics, provide/use services, and interact with other nodes in a ROS 2 network.**
