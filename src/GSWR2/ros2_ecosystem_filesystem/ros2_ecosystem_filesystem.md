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
    <h1>ROS2 Ecosystem and Filesystem: A Comprehensive Guide</h1>
</center>

---

### Introduction

> The Robot Operating System (ROS) is a flexible framework for writing robot software. ROS2, the latest version, brings several improvements over its predecessor, including better support for real-time computing, enhanced security, and improved modularity. Understanding the ROS2 ecosystem and filesystem is crucial for effectively developing and managing robot applications. In this blog post, we'll explore the ROS2 underlay and overlay workspace environments, create a Colcon workspace, explain the build and install files, and create custom ROS2 packages using both Python and CMake.

### ROS2 Underlay and Overlay Workspace Environment

> *In ROS2, the concept of workspaces is essential for organizing and managing different projects and dependencies. There are two primary types of workspaces:*

1. **Underlay Workspace**: This is the base workspace where core ROS2 packages and other dependencies are installed. It serves as the foundation for overlay workspaces. Typically, this includes the installation of ROS2 itself and any third-party libraries that your project depends on. It is located inside the `/opt/ros/humble/` directory.

    <img src="resources/underlay.png" />

2. **Overlay Workspace**: This workspace sits on top of the underlay workspace. It is used for developing and testing your own packages. Overlay workspaces can be layered on top of each other, allowing for flexible development and testing environments. We will create an overlay workspace for the project in this tutorial below.

### Creating a Colcon Workspace

> Colcon is a command-line tool used to build, test, and package ROS2 applications. It is designed to work with multiple build systems and is essential for managing ROS2 workspaces. Here's how to create a Colcon workspace:

1. **Set Up Your Environment**: Ensure you have ROS2 and Colcon installed. You can install ROS2 following the instructions from the [ROS2 documentation](https://docs.ros.org/en/foxy/Installation.html) or previous module of this course [here](../introduction_installation/intro_install.md). Install Colcon using pip:

   ```bash
   pip install -U colcon-common-extensions
   ```

2. **Create the Workspace Directory**: Create a new directory for your workspace and navigate into it:

   ```bash
   mkdir -p ~/ros2_ws/src
   cd ~/ros2_ws
   ```

   > ***Tip:** You can name your workspace whatever you want. However, it is recommended to name it as per your project details.*

3. **Initialize the Workspace**: Use Colcon to initialize your workspace:

   ```bash
   colcon build
   ```

   This command will set up the necessary directories and files for your workspace.

### Build and Install File Explanation

When you build a ROS2 workspace using Colcon, several directories and files are generated:

- **build/**: This directory contains intermediate build files and artifacts for each package.
- **install/**: This directory contains the installed files for each package. It mimics the structure of the system's file hierarchy, making it easier to locate executables, libraries, and other resources.
- **log/**: This directory stores log files generated during the build and test processes.

> ***Note:** Whenever you make changes to your packages, you must re-build your workspace before running your applications and source your setup files to make your packages available.*

### Creating a Custom ROS2 Package (Python and CMake)

> *Creating custom packages is a fundamental part of developing with ROS2. Here's how to create a simple package using both Python and CMake.*

#### Creating a Python Package

1. **Create the Package**: Navigate to the `src` directory of your workspace and create a new package:

   ```bash
   cd ~/ros2_ws/src
   ros2 pkg create --build-type ament_python my_python_pkg
   ```

   This command creates a new directory `my_python_pkg` with the necessary files and directories.

2. **Package Structure**: The package structure will look like this:

   ```
   my_python_pkg/
   ├── package.xml
   ├── setup.cfg
   ├── setup.py
   └── my_python_pkg
       └── __init__.py
   ```

3. **Edit setup.py**: Define the package metadata and entry points in `setup.py`:

   ```python
   from setuptools import setup

   package_name = 'my_python_pkg'

   setup(
       name=package_name,
       version='0.0.0',
       packages=[package_name],
       data_files=[
           ('share/ament_index/resource_index/packages',
               ['resource/' + package_name]),
           ('share/' + package_name, ['package.xml']),
       ],
       install_requires=['setuptools'],
       zip_safe=True,
       maintainer='Your Name',
       maintainer_email='your.email@example.com',
       description='Example Python package for ROS2',
       license='Apache License 2.0',
       tests_require=['pytest'],
       entry_points={
           'console_scripts': [
               'talker = my_python_pkg.talker:main',
               'listener = my_python_pkg.listener:main',
           ],
       },
   )
   ```

4. **Create Python Nodes**: Add your Python nodes in the `my_python_pkg` directory. For example, create `talker.py` and `listener.py`:

   ```python
   # talker.py
   import rclpy
   from rclpy.node import Node
   from std_msgs.msg import String

   class Talker(Node):
       def __init__(self):
           super().__init__('talker')
           self.publisher_ = self.create_publisher(String, 'chatter', 10)
           self.timer = self.create_timer(0.5, self.timer_callback)

       def timer_callback(self):
           msg = String()
           msg.data = 'Hello, ROS2!'
           self.publisher_.publish(msg)
           self.get_logger().info('Publishing: "%s"' % msg.data)

   def main(args=None):
       rclpy.init(args=args)
       node = Talker()
       rclpy.spin(node)
       node.destroy_node()
       rclpy.shutdown()

   if __name__ == '__main__':
       main()
   ```

   ```python
   # listener.py
   import rclpy
   from rclpy.node import Node
   from std_msgs.msg import String

   class Listener(Node):
       def __init__(self):
           super().__init__('listener')
           self.subscription = self.create_subscription(
               String,
               'chatter',
               self.listener_callback,
               10)
           self.subscription  # prevent unused variable warning

       def listener_callback(self, msg):
           self.get_logger().info('I heard: "%s"' % msg.data)

   def main(args=None):
       rclpy.init(args=args)
       node = Listener()
       rclpy.spin(node)
       node.destroy_node()
       rclpy.shutdown()

   if __name__ == '__main__':
       main()
   ```

#### Creating a CMake Package

1. **Create the Package**: Navigate to the `src` directory of your workspace and create a new package:

   ```bash
   cd ~/ros2_ws/src
   ros2 pkg create --build-type ament_cmake my_cpp_pkg
   ```

   This command creates a new directory `my_cpp_pkg` with the necessary files and directories.

2. **Package Structure**: The package structure will look like this:

   ```
   my_cpp_pkg/
   ├── CMakeLists.txt
   ├── package.xml
   └── src
       └── main.cpp
   ```

3. **Edit CMakeLists.txt**: Define the build instructions in `CMakeLists.txt`:

   ```cmake
   cmake_minimum_required(VERSION 3.5)
   project(my_cpp_pkg)

   # Default to C++14
   if(NOT CMAKE_CXX_STANDARD)
     set(CMAKE_CXX_STANDARD 14)
   endif()

   # find dependencies
   find_package(ament_cmake REQUIRED)
   find_package(rclcpp REQUIRED)
   find_package(std_msgs REQUIRED)

   add_executable(talker src/talker.cpp)
   ament_target_dependencies(talker rclcpp std_msgs)

   add_executable(listener src/listener.cpp)
   ament_target_dependencies(listener rclcpp std_msgs)

   install(TARGETS
     talker
     listener
     DESTINATION lib/${PROJECT_NAME})

   ament_package()
   ```

4. **Create C++ Nodes**: Add your C++ nodes in the `src` directory. For example, create `talker.cpp` and `listener.cpp`:

   ```cpp
   // talker.cpp
   #include "rclcpp/rclcpp.hpp"
   #include "std_msgs/msg/string.hpp"

   using namespace std::chrono_literals;

   class Talker : public rclcpp::Node
   {
   public:
     Talker()
       : Node("talker")
     {
       publisher_ = this->create_publisher<std_msgs::msg::String>("chatter", 10);
       timer_ = this->create_wall_timer(
         500ms, std::bind(&Talker::timer_callback, this));
     }

   private:
     void timer_callback()
     {
       auto message = std_msgs::msg::String();
       message.data = "Hello, ROS2!";
       publisher_->publish(message);
       RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
     }
     rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
     rclcpp::TimerBase::SharedPtr timer_;
   };

   int main(int argc, char * argv[])
   {
     rclcpp::init(argc, argv);
     rclcpp::spin(std::make_shared<Talker>());
     rclcpp::shutdown();
     return 0;
   }
   ```

   ```cpp
   // listener.cpp
   #include "rclcpp/rclcpp.hpp"
   #include "std_msgs/msg/string.hpp"

   class Listener : public rclcpp::Node
   {
   public:
     Listener()
       : Node("listener")
     {
       subscription_ = this->create_subscription<std_msgs::msg::String>(
         "chatter", 10, std::bind(&Listener

</br>

-------