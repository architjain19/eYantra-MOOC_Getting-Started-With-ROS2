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
    <h1>ROS 2 Launch</h1>
</center>

---

## Description:

A ROS 2 system typically consists of many nodes running across many different processes (and even different machines). While it is possible to run each of these nodes separately, it gets cumbersome quite quickly.

The launch system in ROS 2 is meant to automate the running of many nodes with a single command. It helps the user describe the configuration of their system and then executes it as described. The configuration of the system includes what programs to run, where to run them, what arguments to pass them, and ROS-specific conventions which make it easy to reuse components throughout the system by giving them each a different configuration. It is also responsible for monitoring the state of the processes launched, and reporting and/or reacting to changes in the state of those processes.

All of the above is specified in a launch file, which can be written in Python, XML, or YAML. This launch file can then be run using the `ros2 launch` command, and all of the nodes specified will be run.

## Motivation:

In most of the introductory tutorials, you have been opening new terminals for every new node you run. As you create more complex systems with more and more nodes running simultaneously, opening terminals and reentering configuration details becomes tedious.

Launch files allow you to start up and configure a number of executables containing ROS 2 nodes simultaneously.

Running a single launch file with the ros2 launch command will start up your entire system - all nodes and their configurations - at once.


### Running a Launch File:

Open a new terminal and run:

```sh
ros2 launch turtlesim multisim.launch.py
```

This command will run the following launch file:

```sh
# turtlesim/launch/multisim.launch.py

from launch import LaunchDescription
import launch_ros.actions

def generate_launch_description():
    return LaunchDescription([
        launch_ros.actions.Node(
            namespace= "turtlesim1", package='turtlesim', executable='turtlesim_node', output='screen'),
        launch_ros.actions.Node(
            namespace= "turtlesim2", package='turtlesim', executable='turtlesim_node', output='screen'),
    ])
```

> **Note:** The launch file above is written in Python, but you can also use XML and YAML to create launch files. You can see a comparison of these different ROS 2 launch formats in [Using Python, XML, and YAML for ROS 2 Launch Files](https://docs.ros.org/en/humble/How-To-Guides/Launch-file-different-formats.html).

This will run two turtlesim nodes:

<img src="https://docs.ros.org/en/humble/_images/turtlesim_multisim.png" />

You can find more information on ROS 2 launch in the [ROS 2 launch tutorials](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Launch-Main.html).

The significance of what you’ve done so far is that you’ve run two turtlesim nodes with one command. Once you learn to write your own launch files, you’ll be able to run multiple nodes - and set up their configuration - in a similar way, with the `ros2 launch` command.


### Write the launch file

Let’s put together a ROS 2 launch file using the `turtlesim` package and its executables. As mentioned above, this can either be in Python, XML, or YAML.

* launch/turtlesim_mimic_launch.py

    ```sh
    from launch import LaunchDescription
    from launch_ros.actions import Node

    def generate_launch_description():
        return LaunchDescription([
            Node(
                package='turtlesim',
                namespace='turtlesim1',
                executable='turtlesim_node',
                name='sim'
            ),
            Node(
                package='turtlesim',
                namespace='turtlesim2',
                executable='turtlesim_node',
                name='sim'
            ),
            Node(
                package='turtlesim',
                executable='mimic',
                name='mimic',
                remappings=[
                    ('/input/pose', '/turtlesim1/turtle1/pose'),
                    ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
                ]
            )
        ])
    ```

* launch/turtlesim_mimic_launch.xml
    ```sh
    <launch>
    <node pkg="turtlesim" exec="turtlesim_node" name="sim" namespace="turtlesim1"/>
    <node pkg="turtlesim" exec="turtlesim_node" name="sim" namespace="turtlesim2"/>
    <node pkg="turtlesim" exec="mimic" name="mimic">
        <remap from="/input/pose" to="/turtlesim1/turtle1/pose"/>
        <remap from="/output/cmd_vel" to="/turtlesim2/turtle1/cmd_vel"/>
    </node>
    </launch>
    ```

* launch/turtlesim_mimic_launch.yaml
    ```sh
    launch:

    - node:
        pkg: "turtlesim"
        exec: "turtlesim_node"
        name: "sim"
        namespace: "turtlesim1"

    - node:
        pkg: "turtlesim"
        exec: "turtlesim_node"
        name: "sim"
        namespace: "turtlesim2"

    - node:
        pkg: "turtlesim"
        exec: "mimic"
        name: "mimic"
        remap:
        -
            from: "/input/pose"
            to: "/turtlesim1/turtle1/pose"
        -
            from: "/output/cmd_vel"
            to: "/turtlesim2/turtle1/cmd_vel"
    ```

### Examine the Launch File

We will look for explanation in python, you can refer [this tutorial](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Creating-Launch-Files.html) for other formats.

These import statements pull in some Python `launch` modules.
```sh
from launch import LaunchDescription
from launch_ros.actions import Node
```

Next, the launch description itself begins:

```sh
def generate_launch_description():
   return LaunchDescription([

   ])
```

The first two actions in the launch description launch the two turtlesim windows:
```sh
Node(
    package='turtlesim',
    namespace='turtlesim1',
    executable='turtlesim_node',
    name='sim'
),
Node(
    package='turtlesim',
    namespace='turtlesim2',
    executable='turtlesim_node',
    name='sim'
),
```

The final action launches the mimic node with the remaps:

```sh
Node(
    package='turtlesim',
    executable='mimic',
    name='mimic',
    remappings=[
      ('/input/pose', '/turtlesim1/turtle1/pose'),
      ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
    ]
)
```

### ros2 launch

To run the launch file created above, enter into the directory you created earlier and run the following command:

- Python
    ```sh
    cd launch
    ros2 launch turtlesim_mimic_launch.py
    ```

- XML
    ```sh
    cd launch
    ros2 launch turtlesim_mimic_launch.xml
    ```

- YAML
    ```sh
    cd launch
    ros2 launch turtlesim_mimic_launch.yaml
    ```

> **Note:** It is possible to launch a launch file directly (as we do above), or provided by a package. When it is provided by a package, the syntax is:
> ```sh
> ros2 launch <package_name> <launch_file_name>
> ```

> **Note:** For packages with launch files, it is a good idea to add an `exec_depend` dependency on the `ros2launch` package in your package’s `package.xml`:
> ```sh
> <exec_depend>ros2launch</exec_depend>
> ```
> This helps make sure that the `ros2 launch` command is available after building your package. It also ensures that all [launch file formats](https://docs.ros.org/en/humble/How-To-Guides/Launch-file-different-formats.html) are recognized.


## References:

- [Creating Launch Files](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Creating-Launch-Files.html)

- [Launching Multiple Nodes](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Launching-Multiple-Nodes/Launching-Multiple-Nodes.html)

</br>

---