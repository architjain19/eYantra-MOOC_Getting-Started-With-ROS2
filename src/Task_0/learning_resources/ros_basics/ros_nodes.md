<!-- <center><img src="http://mooc.e-yantra.org/img/eYantra_logo.svg" alt="e-yantra_logo" style="scale:75%;" /></center> -->

<style>
.back{
	position: fixed;
	width: 250px;
	height: 250px;
	top: 50%;
	left: 50%;
    margin-top: auto; 
    margin-left: auto; 
	opacity: 0.15;
    z-index: -1;
	}
</style>
<!-- <img src="http://mooc.e-yantra.org/img/EyantraLogoMini.png" class="back"> -->

<center>
    <h1>ROS 2 Nodes</h1>
</center>

---

</br>

A node is a participant in the ROS 2 graph, which uses a [client library](https://docs.ros.org/en/humble/Concepts/Basic/About-Client-Libraries.html) to communicate with other nodes. Nodes can communicate with other nodes within the same process, in a different process, or on a different machine. Nodes are typically the unit of computation in a ROS graph; each node should do one logical thing.

Nodes can [publish](https://docs.ros.org/en/humble/Concepts/Basic/About-Topics.html) to named topics to deliver data to other nodes, or [subscribe](https://docs.ros.org/en/humble/Concepts/Basic/About-Topics.html) to named topics to get data from other nodes. They can also act as a [service client](https://docs.ros.org/en/humble/Concepts/Basic/About-Services.html) to have another node perform a computation on their behalf, or as a [service server](https://docs.ros.org/en/humble/Concepts/Basic/About-Services.html) to provide functionality to other nodes. For long-running computations, a node can act as an [action client](https://docs.ros.org/en/humble/Concepts/Basic/About-Actions.html) to perform it, or as an [action server](https://docs.ros.org/en/humble/Concepts/Basic/About-Actions.html) to have another node perform it. Nodes can provide configurable [parameters](https://docs.ros.org/en/humble/Concepts/Basic/About-Parameters.html) to change behavior during run-time.

Connections between nodes are established through a distributed [discovery](https://docs.ros.org/en/humble/Concepts/Basic/About-Discovery.html) process.

Each node in ROS should be responsible for a single, modular purpose, e.g. controlling the wheel motors or publishing the sensor data from a laser range-finder. Each node can send and receive data from other nodes via topics, services, actions, or parameters.

<img src="https://docs.ros.org/en/humble/_images/Nodes-TopicandService.gif">

A full robotic system is comprised of many nodes working in concert. In ROS 2, a single executable (C++ program, Python program, etc.) can contain one or more nodes.

## ROS 2 Node Commands:

### ros2 run

The command `ros2 run` launches an executable from a package.

```sh
ros2 run <package_name> <executable_name>
```

To run turtlesim, open a new terminal, and enter the following command:

```sh
ros2 run turtlesim turtlesim_node
```

The turtlesim window will open, where the package name is `turtlesim` and the executable name is `turtlesim_node`.

We still don’t know the node name, however. You can find node names by using `ros2 node list`


### ros2 node list

`ros2 node list` will show you the names of all running nodes. This is especially useful when you want to interact with a node, or when you have a system running many nodes and need to keep track of them.

Open a new terminal while turtlesim is still running in the other one, and enter the following command:
```sh
ros2 node list
```

The terminal will return the node name:

```sh
/turtlesim
```

Open another new terminal and start the teleop node with the command:

```sh
ros2 run turtlesim turtle_teleop_key
```

Here, we are referring to the `turtlesim` package again, but this time we target the executable named `turtle_teleop_key`.

Return to the terminal where you ran `ros2 node list` and run it again. You will now see the names of two active nodes:

```sh
/turtlesim
/teleop_turtle
```


### ros2 node info

Now that you know the names of your nodes, you can access more information about them with:

```sh
ros2 node info <node_name>
```

To examine your latest node, `my_turtle`, run the following command:

```sh
ros2 node info /my_turtle
```

`ros2 node info` returns a list of subscribers, publishers, services, and actions. i.e. the ROS graph connections that interact with that node. The output should look like this:

```sh
/my_turtle
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /my_turtle/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /my_turtle/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /my_turtle/get_parameters: rcl_interfaces/srv/GetParameters
    /my_turtle/list_parameters: rcl_interfaces/srv/ListParameters
    /my_turtle/set_parameters: rcl_interfaces/srv/SetParameters
    /my_turtle/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
  Service Clients:

  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:
```

Now try running the same command on the `/teleop_turtle` node, and see how its connections differ from `my_turtle`.


## References:

- [About Nodes](https://docs.ros.org/en/humble/Concepts/Basic/About-Nodes.html)

- [Understanding ROS 2 Nodes](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html)

</br>

---