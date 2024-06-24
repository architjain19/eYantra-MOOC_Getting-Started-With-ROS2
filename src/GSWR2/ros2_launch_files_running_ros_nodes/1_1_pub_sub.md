
## Writing a simple publisher and subscriber

### 1. Source ROS 2 environment
```bash
source /opt/ros/humble/setup.bash
```

### 2. Create a new directory
Open a new terminal and source your ROS 2 installation so that ros2 commands will work.

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```
### 3. Create a package

**NOTE: Packages should be created in the src directory, not the root of the workspace. So, navigate into ros2_ws/src, and run the package creation command:**

```bash
ros2 pkg create --build-type ament_python py_pubsub
```

### 4. Write the publisher node
**Navigate into ros2_ws/src/py_pubsub/py_pubsub**

- Open it in your favorite code editior 

### 5. create a file named publisher.py

```bash 
# The first lines of code after the comments 
# import rclpy so its Node class can be used.
import rclpy
from rclpy.node import Node

# The next statement imports the built-in string 
# message type that the node uses to structure the data that it passes on the topic.
from std_msgs.msg import String


# Next, the MyPublisher class is created, 
# which inherits from (or is a subclass of) Node.
class Publisher(Node):
    def __init__(self):
        super().__init__('publisher')

        #create_publisher declares that the node publishes messages 
        # of type String (imported from the std_msgs.msg module), over 
        # a topic named topic, and that the “queue size” is 10. 
        # Queue size is a required QoS (quality of service) setting that 
        # limits the amount of queued messages if a subscriber is not receiving them fast enough.
        self.publisher_ = self.create_publisher(String, 'topic_name', 10)
        
        #timer is created with a callback to execute every 0.5 seconds
        self.timer = self.create_timer(0.5, self.timer_callback)  # 0.5 seconds

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello, world!'
        self.publisher_.publish(msg)

def main(args=None):
    rclpy.init(args=args)
    publisher = Publisher()
    rclpy.spin(publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    publisher.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```


### 6. create a file named subscriber.py

```bash
# The subscriber node’s code is nearly identical to the publisher’s. 
# The constructor creates a subscriber with the same arguments as the publisher.


# the topic name and message type used by the publisher and subscriber must match to allow them to communicate.

import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class Subscriber(Node):
    def __init__(self):
        super().__init__('subscriber')

        # The subscriber’s constructor and callback don’t include any timer definition, 
        # because it doesn’t need one. Its callback gets called as soon as it receives a message.
        self.subscription = self.create_subscription(
            String,
            'topic_name',
            self.listener_callback,
            10
        )

    # The callback definition simply prints an info message to the console, 
    # along with the data it received. 
    def listener_callback(self, msg):
        self.get_logger().info(f'I heard: "{msg.data}"')

def main(args=None):
    rclpy.init(args=args)
    subscriber = Subscriber()
    rclpy.spin(subscriber)
    subscriber.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### 7. Add dependencies

- Navigate one level back to the ros2_ws/src/py_pubsub directory, where the setup.py, setup.cfg, and package.xml files have been created for you.

- Open package.xml with your text editor.



```bash
<description>Examples of minimal publisher/subscriber using rclpy</description>
<maintainer email="you@email.com">Your Name</maintainer>
<license>Apache License 2.0</license>
```

**After the lines above, add the following dependencies corresponding to your node’s import statements:**



```bash
<exec_depend>rclpy</exec_depend>
<exec_depend>std_msgs</exec_depend>
```

**This declares the package needs rclpy and std_msgs when its code is executed.**

## 8. Add an entry point

- Open the setup.py file. Again, match the maintainer, maintainer_email, description and license fields to your package.xml:

```bash
maintainer='YourName',
maintainer_email='you@email.com',
description='Examples of minimal publisher/subscriber using rclpy',
license='Apache License 2.0',
```

Add the following line within the console_scripts brackets of the entry_points field:

```bash
entry_points={
    'console_scripts': [
        'publisher = py_pubsub.publisher:main',
        'subscriber = py_pubsub.subscriber:main',
    ],
},
```

## 9. Build
You likely already have the rclpy and std_msgs packages installed as part of your ROS 2 system. It’s good practice to run rosdep in the root of your workspace (ros2_ws) to check for missing dependencies before building:

```bash
rosdep install -i --from-path src --rosdistro humble -y
```

Still in the root of your workspace, ros2_ws, build your new package:
```bash
colcon build
```
Open a new terminal, navigate to ros2_ws, and source the setup files:
```bash
source install/setup.bash
```
## 10. Now run the talker node:
```bash
ros2 run py_pubsub publisher
```

- Open another terminal, source the setup files from inside ros2_ws again, and then start the listener node:

```bash
ros2 run py_pubsub subscriber
```

## Summary
**You created two nodes to publish and subscribe to data over a topic**