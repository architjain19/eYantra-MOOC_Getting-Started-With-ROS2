## Creating a Second Turtle and Controlling it with ros2 topic pub

## Overview

This guide will walk you through the steps to create a second turtle in the Turtlesim simulation and control it using the `ros2 topic pub` command. You will also learn how to install and use `rqt` to interact with ROS services.

## Step-by-Step Guide

## Method 1

### Step 1: Install rqt

First, ensure your system's package list is updated and install all `rqt` related packages:

```bash
sudo apt update
sudo apt install ~nros-humble-rqt*
```

### Step 2: Install rqt
To start Turtlesim, enter the following command in your terminal:

```bash
ros2 run turtlesim turtlesim_node
```
This will open the Turtlesim window with a default turtle in the center.

### Step 3: Use rqt to Spawn a Second Turtle

#### Open rqt
After installation, start rqt by simply typing:

```bash
rqt
```
When you run 'rqt' for the first time, the window will be blank. Follow these steps to use the service caller plugin to spawn a second turtle:

#### Open Service Caller Plugin

In the rqt window, go to the menu bar and select Plugins > Services > Service Caller.

#### Select the Spawn Service

In the Service Caller panel, you will see a dropdown menu. Select the /spawn service. This is the service provided by Turtlesim to create a new turtle.

#### Configure the Spawn Service

You will see fields to input the parameters for the service. Fill in the fields as follows:

- x : 5.0
- y : 5.0
- theta : 0.0
- name : turtle2

Click the Call button to send the request. If successful, you will see a new turtle appear on the screen at the specified coordinates.


### Step 4: Publish Velocity Commands to Control the Second Turtle

Open a new terminal and publish velocity commands to the second turtle's command topic using 'ros2 topic pub':

```bash
ros2 topic pub /turtle2/cmd_vel geometry_msgs/msg/Twist "
{linear: {x: -2.0, y: -2.0, z: 0.0}, 
angular: {x: 0.0, y: 0.0, z: 1.0}}"
```

#### Explanation 

The 'ros2 topic pub' command publishes a single message to the specified topic. Here, you are sending a 'Twist' message to the '/turtle2/cmd_vel' topic with the following values:

- 'linear' : Sets the linear velocity of the turtle.
    - - x : -3.0 (move backward)
    - - y : -3.0 (move left, though Turtlesim typically only uses x for forward/backward movement)
    - - z : 0.0 (no movement in the z direction)
- 'angular' : Sets the angular velocity of the turtle.
    - - x : 0.0 (no rotation around the x-axis)
    - - y : 0.0 (no rotation around the y-axis)
    - - z : 2.0 (rotate counter-clockwise around the z-axis)

    

## Method 2

### Step 1: Start the Turtlesim Node

First, you need to start the Turtlesim simulation:
```bash
ros2 run turtlesim turtlesim_node
```

### Step 2: Spawn a Second Turtle

Next, you will spawn a second turtle using the /spawn service. Open a new terminal and run the following command:

```bash
ros2 service call /spawn turtlesim/srv/Spawn "{x: 5.0, y: 5.0, theta: 0.0, name: 'turtle2'}"
```
This command will create a second turtle at coordinates (5.0, 5.0) with an orientation of 0 radians, named turtle2.



### Step 3: Publish a Velocity Command to Control the First Turtle

Now, you can control the first turtle by publishing velocity commands to its topic. Use the following command to move turtle2:

```bash
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.0}}"
```

### Step 3: Publish a Velocity Command to Control the Second Turtle

Now, you can control the second turtle by publishing velocity commands to its topic. Use the following command to move turtle2:

```bash
ros2 topic pub /turtle2/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.5}}"
```

This command sets the linear velocity to 2.0 (moving forward) and the angular velocity to 1.0 (turning).


### Conclusion
#### You have successfully created a second turtle in the Turtlesim simulation and controlled it using the ros2 topic pub command. You also learned how to use rqt to interact with ROS services, making it easier to work with ROS functionalities through a graphical interface.
#### By following these steps, you can expand your understanding and control of the Turtlesim simulation and apply these skills to more complex ROS 2 projects.