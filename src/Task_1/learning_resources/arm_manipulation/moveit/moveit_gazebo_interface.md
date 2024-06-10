# Gazebo Interface
> **NOTE**: Package & file names, and content of config files might be slightly different.
* Now that we have seen how to use Setup assistant and visualize the movement of the arm in Rviz, let's find out how to simulate it in Gazebo. 
* To make the arm move on Gazebo we need an interface that will take the commands from move_it and convey it to the arm in simulation.
* This interface in this scenario is a controller. The controller is basically a generic control loop feedback mechanism, typically a PID controller, to control the output sent to your actuators.

### We need to add the following:
##### 1. ROS Controllers
- A configuration file called `ros_controllers.yaml` has to be created inside the `config` folder of the `ur5_moveit` package, and copy the code given below.
- This is for ROS to know about the controllers and its specification.
- Remove the previous contents (`if any`) and paste the configuration given below.

*Example reference Link: [Description for Joint trajetory controller](https://control.ros.org/master/doc/ros2_controllers/joint_trajectory_controller/doc/userdoc.html)*
```yaml
controller_manager:
  ros__parameters:
    update_rate: 2000 #1500  # Hz 1500
    joint_trajectory_controller:
      type: joint_trajectory_controller/JointTrajectoryController
    joint_state_broadcaster:
      type: joint_state_broadcaster/JointStateBroadcaster

# parameters for each controller listed under controller manager
joint_trajectory_controller:
  ros__parameters:
    command_interfaces:
      - position
    state_interfaces:
      - position
      - velocity
    joints:
      - elbow_joint
      - shoulder_lift_joint
      - shoulder_pan_joint
      - wrist_1_joint
      - wrist_2_joint
      - wrist_3_joint
    state_publish_rate: 100.0
    action_monitor_rate: 20.0
    allow_partial_joints_goal: false
    constraints:
      stopped_velocity_tolerance: 0.0
      goal_time: 0.0

joint_state_broadcaster:
  ros__parameters:
    type: joint_state_broadcaster/JointStateBroadcaster
```
##### 2. Moveit Controllers
- A configuration file called `moveit_controllers.yaml` has to be created inside the `config` folder of the `ur5_moveit` package, and copy the code given below.
- This file is specifically for Moveit to know about the controller.
- We encourage to find more details in the Moveit's documentation.
- Remove the previous contents (`if any`) and paste the configuration given below.
```yaml
controller_names:
  - joint_trajectory_controller

joint_trajectory_controller:
  action_ns: follow_joint_trajectory
  type: FollowJointTrajectory
  default: true
  joints:
    - shoulder_pan_joint
    - shoulder_lift_joint
    - elbow_joint
    - wrist_1_joint
    - wrist_2_joint
    - wrist_3_joint
```
##### 3. OMPL Planning
- A configuration file called `ompl_planning.yaml` has to be created inside the `config` folder of the `ur5_moveit` package, and copy the code given below.
- For basic implementation we are using OMPL as the planning method for UR5, you are free to experiment with different planner methods.
- Remove the previous contents (`if any`) and paste the configuration given below.
```yaml
planning_plugin: 'ompl_interface/OMPLPlanner'
request_adapters: >-
    default_planner_request_adapters/AddTimeOptimalParameterization
    default_planner_request_adapters/FixWorkspaceBounds
    default_planner_request_adapters/FixStartStateBounds
    default_planner_request_adapters/FixStartStateCollision
    default_planner_request_adapters/FixStartStatePathConstraints
start_state_max_bounds_error: 0.1
```
##### 4. Servo Information
- A configuration file called `ur_servo.yaml` has to be created inside the `config` folder of the `ur5_moveit` package, and copy the code given below.
- This file states about all the configuration while servoing robotic arm, more about it in the upcoming sections.
- Remove the previous contents (`if any`) and paste the configuration given below, make sure to check with any naming difference with your setup.
- Referance [link](https://moveit.picknik.ai/humble/doc/examples/realtime_servo/realtime_servo_tutorial.html#servo-configs)
```yaml
###############################################
# Modify all parameters related to servoing here
###############################################
use_gazebo: true # Whether the robot is started in a Gazebo simulation environment

## Properties of incoming commands
command_in_type: "speed_units" # "unitless"> in the range [-1:1], as if from joystick. "speed_units"> cmds are in m/s and rad/s
scale:
  # Scale parameters are only used if command_in_type=="unitless"
  linear:  0.6  # Max linear velocity. Meters per publish_period. Unit is [m/s]. Only used for Cartesian commands.
  rotational:  0.3 # Max angular velocity. Rads per publish_period. Unit is [rad/s]. Only used for Cartesian commands.
  # Max joint angular/linear velocity. Rads or Meters per publish period. Only used for joint commands on joint_command_in_topic.
  joint: 0.01
# This is a fudge factor to account for any latency in the system, e.g. network latency or poor low-level
# controller performance. It essentially increases the timestep when calculating the target pose, to move the target
# pose farther away. [seconds]
system_latency_compensation: 0.04

## Properties of outgoing commands
publish_period: 0.004  # 1/Nominal publish rate [seconds]
low_latency_mode: false  # Set this to true to publish as soon as an incoming Twist command is received (publish_period is ignored)

# What type of topic does your robot driver expect?
# Currently supported are std_msgs/Float64MultiArray or trajectory_msgs/JointTrajectory
command_out_type: trajectory_msgs/JointTrajectory #std_msgs/Float64MultiArray

# What to publish? Can save some bandwidth as most robots only require positions or velocities
publish_joint_positions: true
publish_joint_velocities: false
publish_joint_accelerations: false

## Plugins for smoothing outgoing commands
smoothing_filter_plugin_name: "online_signal_smoothing::ButterworthFilterPlugin"

## Incoming Joint State properties
low_pass_filter_coeff: 10.0  # Larger --> trust the filtered data more, trust the measurements less.

## MoveIt properties
move_group_name:  ur_manipulator  # Often 'manipulator' or 'arm'
planning_frame: base_link  # The MoveIt planning frame. Often 'base_link' or 'world'

## Other frames
ee_frame_name: tool0  # The name of the end effector link, used to return the EE pose
robot_link_command_frame:  base_link  # commands must be given in the frame of a robot link. Usually either the base or end effector

## Stopping behaviour
incoming_command_timeout:  0.1  # Stop servoing if X seconds elapse without a new command
# If 0, republish commands forever even if the robot is stationary. Otherwise, specify num. to publish.
# Important because ROS may drop some messages and we need the robot to halt reliably.
num_outgoing_halt_msgs_to_publish: 4

## Configure handling of singularities and joint limits
lower_singularity_threshold:  100.0  # Start decelerating when the condition number hits this (close to singularity)
hard_stop_singularity_threshold: 200.0 # Stop when the condition number hits this
joint_limit_margin: 0.1 # added as a buffer to joint limits [radians]. If moving quickly, make this larger.

## Topic names
cartesian_command_in_topic: ~/delta_twist_cmds  # Topic for incoming Cartesian twist commands
joint_command_in_topic: ~/delta_joint_cmds # Topic for incoming joint angle commands
joint_topic: /joint_states
status_topic: ~/status # Publish status to this topic
command_out_topic: /joint_trajectory_controller/joint_trajectory #/forward_position_controller/commands # Publish outgoing commands here

## Collision checking for the entire robot body
check_collisions: true # Check collisions?
collision_check_rate: 5.0 # [Hz] Collision-checking can easily bog down a CPU if done too often.
# Two collision check algorithms are available:
# "threshold_distance" begins slowing down when nearer than a specified distance. Good if you want to tune collision thresholds manually.
# "stop_distance" stops if a collision is nearer than the worst-case stopping distance and the distance is decreasing. Requires joint acceleration limits
collision_check_type: threshold_distance
# Parameters for "threshold_distance"-type collision checking
self_collision_proximity_threshold: 0.01 # Start decelerating when a self-collision is this far [m]
scene_collision_proximity_threshold: 0.02 # Start decelerating when a scene collision is this far [m]
# Parameters for "stop_distance"-type collision checking
collision_distance_safety_factor: 1000.0 # Must be >= 1. A large safety factor is recommended to account for latency
min_allowable_collision_distance: 0.01 # Stop if a collision is closer than this [m]
```

##### 5. Launch file to spawn the arm with UR5 in gazebo
- A launch file has to be created in `launch` folder of `ur5_moveit` package.
- Name the file as `spawn_ur5_launch_moveit.launch.py` and copy the code given below.
- Make sure to look for changes in package names or config file names as per your setup.

```python
import os
import yaml
import launch_ros
from launch import LaunchDescription
from launch_ros.actions import Node
from launch.conditions import IfCondition
from ament_index_python import get_package_share_directory
from launch.actions import IncludeLaunchDescription
from launch.launch_description_sources import PythonLaunchDescriptionSource
from launch.actions import TimerAction


def get_package_file(package, file_path):
    """Get the location of a file installed in an ament package"""
    package_path = get_package_share_directory(package)
    absolute_file_path = os.path.join(package_path, file_path)
    return absolute_file_path

def load_file(file_path):
    """Load the contents of a file into a string"""
    try:
        with open(file_path, 'r') as file:
            return file.read()
    except EnvironmentError: # parent of IOError, OSError *and* WindowsError where available
        return None

def load_yaml(file_path):
    """Load a yaml file into a dictionary"""
    try:
        with open(file_path, 'r') as file:
            return yaml.safe_load(file)
    except EnvironmentError: # parent of IOError, OSError *and* WindowsError where available
        return None

def run_xacro(xacro_file):
    """Run xacro and output a file in the same directory with the same name, w/o a .xacro suffix"""
    urdf_file, ext = os.path.splitext(xacro_file)
    if ext != '.xacro':
        raise RuntimeError(f'Input file to xacro must have a .xacro extension, got {xacro_file}')
    os.system(f'xacro {xacro_file} -o {urdf_file}')
    return urdf_file


def generate_launch_description():
    moveit_config_folder_name = 'ur5_moveit'

    xacro_file = get_package_file(moveit_config_folder_name, 'config/ur5.urdf.xacro')
    urdf_file = run_xacro(xacro_file)
    robot_description_arm = load_file(urdf_file)

    srdf_file = get_package_file(moveit_config_folder_name, 'config/ur5.srdf')
    kinematics_file = get_package_file(moveit_config_folder_name, 'config/kinematics.yaml')
    ompl_config_file = get_package_file(moveit_config_folder_name, 'config/ompl_planning.yaml')
    moveit_controllers_file = get_package_file(moveit_config_folder_name, 'config/moveit_controllers.yaml')
    moveit_servo_file = get_package_file(moveit_config_folder_name, "config/ur_servo.yaml")
    ros_controllers_file = get_package_file('ur5_moveit', 'config/ros_controllers.yaml')

    robot_description_semantic = load_file(srdf_file)
    kinematics_config = load_yaml(kinematics_file)
    ompl_config = load_yaml(ompl_config_file)

    moveit_controllers = {
        'moveit_simple_controller_manager' : load_yaml(moveit_controllers_file),
        'moveit_controller_manager': 'moveit_simple_controller_manager/MoveItSimpleControllerManager'
    }
    trajectory_execution = {
        'moveit_manage_controllers': True,
        'trajectory_execution.allowed_execution_duration_scaling': 1.2,
        'trajectory_execution.allowed_goal_duration_margin': 0.5,
        'trajectory_execution.allowed_start_tolerance': 0.01
    }
    planning_scene_monitor_config = {
        'publish_planning_scene': True,
        'publish_geometry_updates': True,
        'publish_state_updates': True,
        'publish_transforms_updates': True
    }

    # MoveIt node
    move_group_node = Node(
        package='moveit_ros_move_group',
        executable='move_group',
        output='screen',
        parameters=[
            {
                'robot_description': robot_description_arm,
                'robot_description_semantic': robot_description_semantic,
                'robot_description_kinematics': kinematics_config,
                'ompl': ompl_config,
                'planning_pipelines': ['ompl'],
            },
            moveit_controllers,
            trajectory_execution,
            planning_scene_monitor_config,
            {"use_sim_time": True},
        ],
    )

    # Servo node for realtime control
    servo_yaml = load_yaml(moveit_servo_file)
    servo_params = {"moveit_servo": servo_yaml}
    robot_description_s = {"robot_description": robot_description_arm}
    robot_description_semantic_s = {"robot_description_semantic": robot_description_semantic}

    servo_node = Node(
        package="moveit_servo",
        # condition=IfCondition(launch_servo),
        executable="servo_node_main",
        parameters=[
            servo_params,
            robot_description_s,
            robot_description_semantic_s,
        ],
        output="screen",
    )

    # TF information
    robot_state_publisher_arm = Node(
        name='robot_state_publisher',
        package='robot_state_publisher',
        executable='robot_state_publisher',
        output='screen',
        parameters=[{'robot_description': robot_description_arm}],
        remappings=[('robot_description', 'robot_description_ur5')]
    )

    #  Visualization (parameters needed for MoveIt display plugin)
    rviz = Node(
        name='rviz',
        package='rviz2',
        executable='rviz2',
        output='screen',
        parameters=[
            {
                'robot_description': robot_description_arm,
                'robot_description_semantic': robot_description_semantic,
                'robot_description_kinematics': kinematics_config,
            }
        ],
    )
    # Controller manager for realtime interactions
    ros2_control_node = Node(
        package="controller_manager",
        executable="ros2_control_node",
        name="control_node_ros2",
        parameters= [
            {'robot_description': robot_description_arm},
            ros_controllers_file
        ],
        output="screen",
    )

    spawn_controllers_manipulator = Node(
            package="controller_manager", 
            executable="spawner",
            name="spawner_mani",
            arguments=['joint_trajectory_controller'],
            output="screen")
    

    spawn_controllers_state = Node(
            package="controller_manager", 
            executable="spawner",
            arguments=['joint_state_broadcaster'],
            output="screen")



    return LaunchDescription([
        robot_state_publisher_arm,
        TimerAction(period=1.0, 
                    actions=[spawn_controllers_manipulator,
                            spawn_controllers_state,
                            rviz,
                            ros2_control_node,
                            move_group_node,
                            servo_node
                            ]),
        
        ]
    )
```

### Do changes in the following:
##### 1. Initial Position
- This file is responsible for making the initial position of arm accordingly during the launch.
- Change the values accordingly so that the arm is not in collision with any other thing in the world during the launch.
- The file can be found in the name of `initial_positions.yaml` file within the `config` folder of `ur5_moveit` package.
```yaml
initial_positions:
  shoulder_pan_joint: 0.0
  shoulder_lift_joint: -2.39
  elbow_joint: 2.4
  wrist_1_joint: -3.15
  wrist_2_joint: -1.58
  wrist_3_joint: 3.15
```
##### 2. Adding gazebo plugin in XACRO
- Finally, we need to add Gazebo plugin for ROS control in the XACRO file generated by moveit setup assistant.
- To avoid confusion you can replace the whole code into the `xacro` file.
- You can find the file named as `ur5.urdf.xacro` in `config` folder of `ur5_moveit` package.
```xml
<?xml version="1.0"?>
<robot xmlns:xacro="http://www.ros.org/wiki/xacro" name="ur5">

    <!-- adding gazebo plugin with ros controller -->
    <gazebo>
        <plugin name="gazebo_ros2_control" filename="libgazebo_ros2_control.so">
            <parameters>$(find ur5_moveit)/config/ros_controllers.yaml</parameters>
        </plugin>
    </gazebo>
    
    <!-- Import ur5 urdf file -->
    <xacro:include filename="$(find ur_description)/urdf/ur5_arm.urdf.xacro" />
    <xacro:include filename="ur5.ros2_control.xacro" />

    <xacro:ur5_ros2_control name="FakeSystem" initial_positions_file="$(find ur5_moveit)/config/initial_positions.yaml"/>
    

</robot>
```