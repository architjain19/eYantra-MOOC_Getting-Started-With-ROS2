# RViz Interface

In the previous module, you completed the **moveit setup assistant** and successfully generated MoveIt! configuration files.
In this module, you will be using those configuration files for the simulation of the robotic arm.

MoveIt! comes with a plugin for the ROS Visualizer (RViz). The plugin allows you to set up scenes in which the robot will work, generate plans, visualize the output and interact directly with a visualized robot. We will explore the plugin in this tutorial.

Let's start by visualizing the planning of a robotic arm in Rviz.
Launch the demo.launch file from the moveit configuration package that you created.

```sh
ros2 launch ur5_moveit demo.launch.py 
```
- This will launch the robotic arm in Rviz
- You will see a robotic arm and a MotionPlanning display type in Rviz.

> **NOTE:** You will not be able to execute planning motion, because we have not yet set up the controllers for the same. We will do the same in the next step.

----

### Some exciting video 
*(Caution: Only for information, and will not resemble to our setup till now)*

- By seeing the below video you can get an idea, for what you will be doing for the next modules. The video shows the demo with `Panda arm`.
 <iframe width="800" height="400"
    src="https://www.youtube.com/embed/18mouzWyqRo?si=7EHFI4-s6Felz49W">
</iframe> 
