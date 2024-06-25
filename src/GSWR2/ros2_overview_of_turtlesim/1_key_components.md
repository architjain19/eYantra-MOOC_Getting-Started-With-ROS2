## Key Components

### 1. Turtle
The primary entity in the Turtlesim simulation, represented by a graphic of a turtle moving in a 2D space.

### 2. Nodes
Nodes are the basic execution units in ROS that perform computations. In Turtlesim, the key nodes are:

- **Turtlesim Node**: Responsible for the graphical simulation of the turtle. It subscribes to topics to receive movement commands and publishes the turtle's current state.
- **Teleoperation Node (turtle_teleop_key)**: Allows you to control the turtle using keyboard inputs. It publishes velocity commands to the `/turtle1/cmd_vel` topic.

### 3. Topics
Topics are named buses over which nodes exchange messages asynchronously. Key topics in Turtlesim are:

- **/turtle1/cmd_vel**: A topic of type `geometry_msgs/Twist`. Nodes publish velocity commands here to control the turtle's movement.
- **/turtle1/pose**: A topic of type `turtlesim/Pose`. This topic publishes the turtle’s current position and orientation.

### 4. Services
Services in ROS provide a way for nodes to perform synchronous request/reply interactions. Key services in Turtlesim are:

- **/reset**: Resets the turtle's position to the center of the screen.
- **/turtle1/set_pen**: Changes the color and width of the turtle's pen, accepting parameters for red, green, blue values, pen width, and whether to turn the pen on or off.