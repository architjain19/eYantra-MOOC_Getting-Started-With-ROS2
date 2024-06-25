# Overview of ROS 2 CLI Tools


## Detailed Description of Common ROS 2 CLI Commands

### ros2 run
#### Description: Runs a ROS 2 node.

```bash
ros2 run <package_name> <executable_name>
```

### ros2 launch
#### Description: Launches multiple nodes defined in a launch file.

Usage:


```bash
ros2 launch <package_name> <launch_file>
```

Example:

```bash
ros2 launch demo_nodes_cpp talker_listener.launch.py
```
(Launches nodes as defined in the talker_listener.launch.py from the demo_nodes_cpp package)



### ros2 topic
#### Description: Tools for interacting with ROS 2 topics.


Subcommands:
- list: Lists all active topics.
```bash
ros2 topic list
```

- echo: Prints messages from a topic.
```bash
ros2 topic echo /chatter
```

- pub: Publishes a message to a topic.
```bash
ros2 topic pub /chatter std_msgs/msg/String "data: 'Hello, ROS 2'" 
```

- info: Shows information about a topic.
```bash
ros2 topic info /chatter
```

### ros2 service
#### Description: Tools for interacting with ROS 2 services.


Subcommands:
- list: Lists all active services.
```bash
ros2 service list
```

- call: Calls a service
```bash
ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{a: 1, b: 2}"
```

- type: Shows the service type.
```bash
ros2 service type /add_two_ints
```

- info: Shows information about a service.
```bash
ros2 service info /add_two_ints
```

### ros2 node
#### Description: Tools for interacting with ROS 2 nodes.


Subcommands:
- list: Lists all active nodes.
```bash
ros2 node list
```

- info: Shows information about a node.
```bash
ros2 node info /talker
```

- kill: Terminates a node.
```bash
ros2 node kill /talker
```



### ros2 bag
#### Description: Tools for recording and playing back ROS 2 bag files.


Subcommands:
- record: Records topics to a bag file.
```bash
ros2 bag record -o my_bag /chatter /parameter_events
```

- play: Plays back messages from a bag file.
```bash
ros2 bag play my_bag
```

- info: Shows information about a bag file.
```bash
ros2 bag info my_bag
```