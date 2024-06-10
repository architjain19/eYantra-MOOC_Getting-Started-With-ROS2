# Nav2 - Navigation 2

![](./nav2_logo.png)


* [Nav2](https://navigation.ros.org/) is the successor of ROS Navigation Stack, aiming to enable safe and versatile mobile robot navigation for complex tasks in various environments.

* It supports tasks beyond simple point-to-point movement, such as intermediary poses and object following, and is trusted by over 50 companies as a high-quality navigation framework.

* It provides perception, planning, control, localization, visualization, and much more to build highly reliable autonomous systems. 

* Nav2 uses behavior trees to create customized and intelligent navigation behavior via orchestrating many independent modular servers.

* The diagram below will give you a good first-look at the structure of Nav2. 




## Nav2 Tools:

1. **Map Management**: It allows for the loading, serving, recording and storing of maps using the Map Server with `slam-toolbox`.

2. **Localization**: The AMCL (Adaptive Monte Carlo Localization) module helps the robot accurately determine its position on the map with EKF (Extended Kalman Filter).

3. **Costmap Generation**: The Nav2 Costmap 2D converts sensor data into costmap representations of the environment.

4. **Path Planning**: Nav2 Planner assists in planning collision-free paths from one point to another while avoiding obstacles.

4. **Robot Control**: The Nav2 Controller guides the robot along the planned path, ensuring it follows the desired trajectory.

5. **Python3 API**: Nav2 offers a Python3 API for interacting with the framework in a pythonic manner, called `Simple Commander`.


# Detailed content for installation
### 1. [Installations](./nav2_installation.md)
<!-- 2. [MoveIt Setup Assistant](https://discuss.e-yantra.org/t/moveit-setup-assistant/10496)
3. [MoveIt Rviz](https://discuss.e-yantra.org/t/rviz-interface-with-moveit/10497)
4. [MoveIt Gazebo interface](https://discuss.e-yantra.org/t/gazebo-interface-with-moveit/10498) -->



---
##  Reading Assignment

* [Nav2 Concepts](https://navigation.ros.org/concepts/index.html#concepts)
* [Nav2 Documentation](https://navigation.ros.org/index.html)
