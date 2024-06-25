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
    <h1>Hands-on Project with ROS2: Turtlesim Integrative Example</h1>
</center>

---

### Introduction

> This hands-on project will guide you through creating a comprehensive ROS2 application that combines Topics, Services, and Actions using the Turtlesim package. This project is designed to reinforce your understanding of these communication mechanisms and how they can be integrated into a real-world application.

### Project Overview

In this project, we will create a system that:
1. **Publishes** the turtle's pose (position and orientation) to a topic.
2. **Provides a service** to reset the turtle's position to the center of the window.
3. **Implements an action** to move the turtle in a square pattern while providing feedback on its progress.

### Prerequisites

Ensure you have the following installed and set up:
- ROS2 (Humble)
- Turtlesim package

You can install the Turtlesim package using:
```sh
sudo apt-get install ros-<your_ros2_distro>-turtlesim
```

### Step 1: Creating the ROS2 Package

First, create a new ROS2 package for our project.

```sh
ros2 pkg create --build-type ament_python turtle_project
```

Navigate to the package directory:
```sh
cd turtle_project
```

### Step 2: Setting Up Topics

#### Publisher: Turtle Pose

Create a Python script named `turtle_pose_publisher.py` to publish the turtle's pose.

```python
# turtle_pose_publisher.py

import rclpy
from rclpy.node import Node
from turtlesim.msg import Pose
from geometry_msgs.msg import PoseStamped

class TurtlePosePublisher(Node):
    def __init__(self):
        super().__init__('turtle_pose_publisher')
        self.publisher_ = self.create_publisher(PoseStamped, 'turtle/pose', 10)
        self.subscription = self.create_subscription(Pose, 'turtle1/pose', self.pose_callback, 10)

    def pose_callback(self, msg):
        pose_stamped = PoseStamped()
        pose_stamped.header.stamp = self.get_clock().now().to_msg()
        pose_stamped.header.frame_id = 'turtle1'
        pose_stamped.pose.position.x = msg.x
        pose_stamped.pose.position.y = msg.y
        pose_stamped.pose.orientation.z = msg.theta
        self.publisher_.publish(pose_stamped)

def main(args=None):
    rclpy.init(args=args)
    node = TurtlePosePublisher()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### Step 3: Setting Up Services

#### Service: Reset Turtle Position

Create a Python script named `turtle_reset_service.py` to reset the turtle's position.

```python
# turtle_reset_service.py

import rclpy
from rclpy.node import Node
from std_srvs.srv import Empty

class TurtleResetService(Node):
    def __init__(self):
        super().__init__('turtle_reset_service')
        self.srv = self.create_service(Empty, 'reset_turtle', self.reset_turtle_callback)

    def reset_turtle_callback(self, request, response):
        self.get_logger().info('Resetting turtle position to the center...')
        self.reset_turtle()
        return response

    def reset_turtle(self):
        reset_client = self.create_client(Empty, 'reset')
        while not reset_client.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('Reset service not available, waiting again...')
        req = Empty.Request()
        future = reset_client.call_async(req)
        rclpy.spin_until_future_complete(self, future)
        if future.result() is not None:
            self.get_logger().info('Turtle reset successfully!')
        else:
            self.get_logger().error('Failed to reset turtle!')

def main(args=None):
    rclpy.init(args=args)
    node = TurtleResetService()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### Step 4: Setting Up Actions

#### Action: Move Turtle in Square

Create a Python script named `turtle_square_action.py` to move the turtle in a square pattern.

```python
# turtle_square_action.py

import rclpy
from rclpy.node import Node
from rclpy.action import ActionServer
from rclpy.action import ActionClient
from turtlesim.msg import Pose
from turtlesim.srv import TeleportAbsolute
from example_interfaces.action import MoveTurtleSquare
from geometry_msgs.msg import Twist

class TurtleSquareActionServer(Node):
    def __init__(self):
        super().__init__('turtle_square_action_server')
        self.action_server = ActionServer(
            self,
            MoveTurtleSquare,
            'move_turtle_square',
            self.execute_callback
        )
        self.publisher_ = self.create_publisher(Twist, 'turtle1/cmd_vel', 10)

    def execute_callback(self, goal_handle):
        self.get_logger().info('Executing goal...')
        feedback_msg = MoveTurtleSquare.Feedback()
        result = MoveTurtleSquare.Result()
        side_length = goal_handle.request.side_length

        for i in range(4):
            self.move_straight(side_length)
            self.rotate_90_degrees()
            feedback_msg.current_side = i + 1
            goal_handle.publish_feedback(feedback_msg)

        goal_handle.succeed()
        result.success = True
        return result

    def move_straight(self, distance):
        twist = Twist()
        twist.linear.x = 2.0
        self.publisher_.publish(twist)
        self.get_clock().sleep_for(rclpy.duration.Duration(seconds=distance / twist.linear.x))
        twist.linear.x = 0.0
        self.publisher_.publish(twist)

    def rotate_90_degrees(self):
        twist = Twist()
        twist.angular.z = 1.57  # Approx 90 degrees
        self.publisher_.publish(twist)
        self.get_clock().sleep_for(rclpy.duration.Duration(seconds=1))
        twist.angular.z = 0.0
        self.publisher_.publish(twist)

def main(args=None):
    rclpy.init(args=args)
    node = TurtleSquareActionServer()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### Step 5: Running the Project

Create an entry point script `setup.py` in the `turtle_project` package.

```python
# setup.py

from setuptools import setup

package_name = 'turtle_project'

setup(
    name=package_name,
    version='0.0.0',
    packages=[package_name],
    py_modules=[
        'turtle_pose_publisher',
        'turtle_reset_service',
        'turtle_square_action'
    ],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='Your Name',
    maintainer_email='your.email@example.com',
    description='Turtle Project with Topics, Services, and Actions',
    license='Apache License 2.0',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            'turtle_pose_publisher = turtle_project.turtle_pose_publisher:main',
            'turtle_reset_service = turtle_project.turtle_reset_service:main',
            'turtle_square_action = turtle_project.turtle_square_action:main'
        ],
    },
)
```

Finally, build and source your package:
```sh
colcon build
source install/setup.bash
```

#### Running the Nodes

In separate terminals, run each of the nodes:
```sh
# Terminal 1: Run the turtlesim node
ros2 run turtlesim turtlesim_node

# Terminal 2: Run the pose publisher
ros2 run turtle_project turtle_pose_publisher

# Terminal 3: Run the reset service
ros2 run turtle_project turtle_reset_service

# Terminal 4: Run the square action server
ros2 run turtle_project turtle_square_action
```

### Conclusion

> This hands-on project provides a comprehensive example of how to integrate Topics, Services, and Actions in a ROS2 application using Turtlesim. By working through this project, you will gain practical experience in setting up and utilizing these communication mechanisms, reinforcing your understanding and preparing you for more complex real-world applications.

---