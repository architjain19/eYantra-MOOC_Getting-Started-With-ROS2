# Key Components of ROS 2 Launch Files
### Launch files in ROS 2 provide a powerful way to start multiple nodes and configure various aspects of your robotic system. Here are the key components and concepts you need to understand when working with ROS 2 launch files.

- LaunchDescription
- Node
- Remappings
- Event Handlers

### 1. LaunchDescription

It is a container that holds all the launch actions you want to execute. Each action can be a node to be launched, a parameter setting, or other configurations.

**Example**
```bash
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='my_package',
            executable='my_node',
            name='my_node_name',
            output='screen'
        )
    ])
```

### 2. Node
The Node action specifies a ROS 2 node to be launched. It includes several parameters such as the package containing the node, the executable name, node name, output configuration, and more.

```bash
Node(
    package='my_package',
    executable='my_node',
    name='my_node_name',
    output='screen'
)
```
#### Key Arguments:

- package: The name of the package containing the node.
- executable: The name of the executable to run.
- name: The name of the node (optional).
- namespace: The namespace to which the node belongs (optional).
- output: Defines where to send the output of the node ('screen' or 'log').

### 3. Remappings
Remappings allow you to change topic, service, or action names at launch time.

**Example**
```bash 
Node(
    package='my_package',
    executable='my_node',
    name='my_node_name',
    remappings=[
        ('/input/pose', '/turtlesim1/turtle1/pose'),
        ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
    ]
)
```

### 4. Event Handlers
Event handlers allow you to define actions based on certain events during the launch process.

**Example**
```bash
from launch.actions import RegisterEventHandler
from launch.event_handlers import OnProcessExit

RegisterEventHandler(
    OnProcessExit(
        target_action=my_node,
        on_exit=[EmitEvent(event=Shutdown())],
    )
)
```