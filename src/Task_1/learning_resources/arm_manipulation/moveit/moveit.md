# MoveIt!
* [MoveIt!](https://moveit.ros.org/) is a very popular Motion Planning Framework.
* It is a set of packages and tools used for Robotic Manipulation in ROS.
* MoveIt! contains software for manipulation, motion planning, kinematics, collision checking etc.
* It also has a RViz plugin which can be used to perform Motion Planning from RViz itself.
* There are also plenty of Python APIs for Moveit! and ROS which can be used to write ROS Nodes that control Robotic Manipulators.
* In this section we are going to learn how to use MoveIt! with ROS and Gazebo.

## MoveIt! Architecture
![](./move_group.png)
<center>Image from moveit concepts</center>

> **NOTE:** The moveit_commander for python is under development for ROS 2, we will be using other alternatives. 

## `move_group` Node
* This node is the most essential part of MoveIt! which connects all the part of the MoveIt! system together.
* This node collects information from the Robot and passes it to various open source plugins available in MoveIt! which are responsible for Motion Planning, IK etc.
* This node then passes the instructions from these plugins to the Robot controller which makes the robot move.
* Python MoveIt! APIs are used to command the `move_group` node to perform actions such as pick/place, IK, FK, among others. 
* `move_group` uses the **Planning Scene Monitor** to maintain a **planning scene**, which is a representation of the world and the current state of the robot. 

# Detailed content for installation
1. [Installations](./installation.md)
2. [MoveIt Setup Assistant](./moveit_setup_assistant.md)
3. [MoveIt Rviz](./moveit_rviz.md)
4. [MoveIt Gazebo interface](./moveit_gazebo_interface.md)
5. [Control UR5 using Rviz](./control_ur5.md)

---
##  Reading Assignment

* [MoveIt! Concepts](https://moveit.ros.org/documentation/concepts)
* [MoveIt! ROS Humble Documentation](https://moveit.picknik.ai/humble/index.html)
