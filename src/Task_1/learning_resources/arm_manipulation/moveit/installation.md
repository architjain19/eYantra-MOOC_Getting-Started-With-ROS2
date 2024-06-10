# Installations

> **NOTE:** `link` for each topics are added as hyperlink in the points for detailed reference.

#### 1. MoveIt [link](https://moveit.picknik.ai/humble/index.html)
Containing all packages of moveit which are binary built and ready for direct deployement.
```sh
sudo apt install ros-humble-moveit
```
#### 2. Joint State Broadcaster [link](https://index.ros.org/p/joint_state_publisher/)
A package which helps to publish joint states to a topic, making all other dependent node to know about the state of each joints.
```sh
sudo apt install ros-humble-joint-state-publisher
```
#### 3. Joint Trajectory Controller [link](https://control.ros.org/master/doc/ros2_controllers/joint_trajectory_controller/doc/userdoc.html)
A controller which helps to send trajectory messages to robotic arm. The message has all specifications of joint angle values, velocity and effort variables
```sh
sudo apt install ros-humble-joint-trajectory-controller
```
#### 4. Moveit Servo [link](https://moveit.ros.org/moveit/ros2/servo/jog/2020/09/09/moveit2-servo.html)
Package which helps to servo the arm using linear velocity input format of link OR actuating all joint angles.
```sh
sudo apt install ros-humble-moveit-servo
``` 
#### 5. Trimesh
Python package for importing mesh file in rviz, so that the arm understands about the envirnomental collision in its planning scene.
```sh
pip install trimesh
```

#### 6. ROS 2 Control CLI [link](https://control.ros.org/master/doc/ros2_control/doc/index.html)
Ros 2 control CLI package helps to access each controller in terminal in a same way as we access `ros2 topic`.
```sh
sudo apt install ros-humble-ros2controlcli
```