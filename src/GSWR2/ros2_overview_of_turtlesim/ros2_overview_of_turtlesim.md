# Turtlesim in ROS

## Overview

Turtlesim is a simple and interactive simulation tool that is part of the ROS (Robot Operating System) tutorials package. It helps users learn the basic concepts of ROS, such as nodes, topics, services, and parameters, by simulating a turtle that can be moved around a screen.


> **[1. Key Components](1_key_components.md)**
- **Turtlesim's key components include the Turtle, Nodes (Turtlesim and Teleoperation), Topics (/turtle1/cmd_vel and /turtle1/pose), and Services (/reset and /turtle1/set_pen)**
 

> **[2. Turtle Simulator](2_turtle_simulator.md)**
- **To install and run Turtle Simulator**
- **Contents of Turtlesim**
    - Turtlesim Node: A graphical simulator displaying a turtle that moves based on ROS 2 commands.
    - Command Line Tools: Includes tools like turtle_teleop_key to control the turtle using keyboard inputs.
    - ROS 2 Topics and Services: Provides topics (e.g., /turtle1/cmd_vel) and services (e.g., /spawn) for interacting with the turtle's movement and state.


> **[3. Creating a Second Turtle](3_creating_second_turtle.md)**

- Spawn a second turtle using the appropriate service call.
- Publish a velocity command to control the second turtle.


> **[4. Controlling a 2D Turtle with Twist Messages](4_controlling_2D_turtle_twist_messages.md)**

- Spawn a second turtle using the appropriate service call.
- Publish a velocity command to control the second turtle.