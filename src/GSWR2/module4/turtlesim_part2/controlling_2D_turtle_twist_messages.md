## Controlling a 2D Turtle with Twist Messages in ROS2

## 1. Setting Up Your ROS 2 Environment
Ensure your ROS 2 environment is set up as described earlier. Create a new ROS 2 package if you haven't already:

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python turtle_twist_control
```

## 2. Installing Dependencies
Ensure your package depends on rclpy and geometry_msgs by editing setup.py and package.xml.<br />
Add dependencies in package.xml:


```bash
<depend>rclpy</depend>
<depend>geometry_msgs</depend>
<depend>turtlesim</depend>
```
Ensure setup.py includes install_requires=['setuptools', 'rclpy', 'geometry_msgs', 'turtlesim'].

## 3. Creating a Python Script to Control and Spawn Two Turtles

Inside the turtle_twist_control package, create a Python script (dual_turtle_control.py):

```bash
cd ~/ros2_ws/src/turtle_twist_control/turtle_twist_control
touch dual_turtle_control.py
chmod +x dual_turtle_control.py
```

###  Understanding the Code

#### Service Client for Spawning Turtle:

- The script creates a client for the spawn service to spawn the second turtle programmatically.
- It waits for the service to become available and sends a request to spawn the turtle at coordinates (2.0, 2.0) with the name 'turtle2'.

#### Node Initialization (super().__init__):

- The TurtleController class initializes a ROS 2 node named 'turtle_controller'.

#### Publishers Creation (create_publisher):

- Publishers for the /turtle1/cmd_vel and /turtle2/cmd_vel topics with Twist messages are created. These will publish velocity commands for each turtle.

#### Timer Setup (create_timer):

- A timer is set up to call publish_velocity_commands at a rate of 10 Hz.

#### Twist Messages for Both Turtles:

- Defines Twist messages for each turtle and assigns linear and angular velocities.
    - - turtle1_twist sets linear.x to 1.0 and angular.z to 0.5.
    - - turtle2_twist sets linear.x to 0.5 and angular.z to -0.5.


### Code

Open dual_turtle_control.py in your favorite text editor and add the following code:

```bash
import rclpy
from rclpy.node import Node
from geometry_msgs.msg import Twist
from turtlesim.srv import Spawn

class TurtleController(Node):
    def __init__(self):
        super().__init__('turtle_controller')
        
        # Create clients for the spawn service
        self.cli = self.create_client(Spawn, 'spawn')
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        
        # Request to spawn the second turtle
        self.req = Spawn.Request()
        self.req.x = 2.0
        self.req.y = 2.0
        self.req.theta = 0.0
        self.req.name = 'turtle2'
        
        self.future = self.cli.call_async(self.req)
        rclpy.spin_until_future_complete(self, self.future)
        
        if self.future.result() is not None:
            self.get_logger().info(f'Successfully spawned {self.future.result().name}')
        else:
            self.get_logger().error('Failed to spawn turtle2')
        
        # Publishers for both turtles
        self.turtle1_pub = self.create_publisher(Twist, '/turtle1/cmd_vel', 10)
        self.turtle2_pub = self.create_publisher(Twist, '/turtle2/cmd_vel', 10)
        
        # Timer to periodically publish messages
        self.timer = self.create_timer(0.1, self.publish_velocity_commands)
        
    def publish_velocity_commands(self):
        # Create Twist messages for both turtles
        turtle1_twist = Twist()
        turtle2_twist = Twist()
        
        # Turtle 1: Move forward and rotate
        turtle1_twist.linear.x = 1.0
        turtle1_twist.angular.z = 0.5
        
        # Turtle 2: Move forward and rotate
        turtle2_twist.linear.x = 0.5
        turtle2_twist.angular.z = -0.5
        
        # Publish messages
        self.turtle1_pub.publish(turtle1_twist)
        self.turtle2_pub.publish(turtle2_twist)

def main(args=None):
    rclpy.init(args=args)
    turtle_controller = TurtleController()
    
    try:
        rclpy.spin(turtle_controller)
    except KeyboardInterrupt:
        pass
    
    turtle_controller.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()


```

### 5. Building and Running the Script
Build your ROS 2 package:

```bash
cd ~/ros2_ws
colcon build
```

Source your ROS 2 workspace:

```bash
source install/setup.bash
```

Run your script:

```bash
ros2 run turtle_twist_control dual_turtle_control
```

### 7. Conclusion
This tutorial demonstrates how to control two turtles in a TurtleSim environment using Twist messages in ROS 2 and programmatically spawn the second turtle. You can modify the linear.x and angular.z values in dual_turtle_control.py to change the turtles' movement behaviors. Experiment and explore further based on learning goals!
