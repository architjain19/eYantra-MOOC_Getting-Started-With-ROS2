# Moveit Servo
> Reference [Web page link for moveit servo in ROS 2 humble](https://moveit.picknik.ai/humble/doc/examples/realtime_servo/realtime_servo_tutorial.html).

MoveIt Servo allows you to stream End Effector (EEF) velocity commands or actuate joint angle by streaming angular velocity to your manipulator and have it execute them concurrently. This enables teleoperation via a wide range of input schemes, or for other autonomous software to control the robot.

## Example demo of Moveit servo `panda` arm 
*(In our case it will be UR5, and the working will not be same in our case as shown in the video)*
<iframe width="700" height="400"
    src="https://www.youtube.com/embed/MF-_XKpGefY?si=Q2_x0a6NnKdz1Hex">
</iframe> 

### Getting started

- Launch the gazebo and rviz launch file as we did in the previous section [control_ur5](./moveit/control_ur5.md).
- Start the moveit_servo by triggering the service, using the following command:
```sh
ros2 service call /servo_node/start_servo std_srvs/srv/Trigger {}
```
- Now use the topic `/servo_node/delta_twist_cmds` (similar to this) as defined in `servo.yaml` file to publish linear velocity commands to the end-effector. You can set the values of x, y, z to move them accordingly.

- Read more about the servo configuration in this [link](https://moveit.picknik.ai/humble/doc/examples/realtime_servo/realtime_servo_tutorial.html#servo-configs).  
For example to make the ur5 EEF move up:
```sh
ros2 topic pub /servo_node/delta_twist_cmds geometry_msgs/msg/TwistStamped "header: auto
twist:
  linear:
    x: 0.0
    y: 0.0
    z: 0.2
  angular:
    x: 0.0
    y: 0.0
    z: 0.0" -r 125
```

## Practice task 
- Try to move the end-effector in an angular fashion, revolving around its tip. 
> **HINT:** Find out angular x, y, z corresponds to what kind of rotation in end-effector
- Also try out `delta_joint_cmds` commands.