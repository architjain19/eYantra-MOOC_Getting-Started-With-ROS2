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
    <h1>ROS 2 Workspace</h1>
</center>

---

## Prerequisites:

* ***Configure Environment:***

    The ROS 2 development environment needs to be correctly configured before use. This can be done in two ways: either sourcing the setup files in every new shell you open, or adding the source command to your startup script.
    You can refer the tutorial to [configure ros 2 environment.](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Configuring-ROS2-Environment.html)


* ***Install colcon:***

    `colcon` is an iteration on the ROS build tools *catkin_make, catkin_make_isolated, catkin_tools* and *ament_tools*. For more information on the design of colcon see [this document](https://design.ros2.org/articles/build_tool.html).

    ```sh
    sudo apt install python3-colcon-common-extensions
    ```


## Basics:
A workspace is a directory containing ROS 2 packages *(ROS 2 is version name and not two packages)*. Before using ROS 2, it’s necessary to source your ROS 2 installation workspace in the terminal you plan to work in. This makes ROS 2’s packages available for you to use in that terminal.

A ROS workspace is a directory with a particular structure. Commonly there is a `src` subdirectory. Inside that subdirectory is where the source code of ROS packages will be located. Typically the directory starts otherwise empty.

colcon does out of source builds. By default it will create the following directories as peers of the `src` directory:

- The `build` directory will be where intermediate files are stored. For each package a subfolder will be created in which e.g. CMake is being invoked.

- The `install` directory is where each package will be installed to. By default each package will be installed into a separate subdirectory.

- The `log` directory contains various logging information about each colcon invocation.
    
> **Note:** Compared to *catkin* there is no `devel` directory.


### Create a workspace

First, create a directory (`ros2_ws`) to contain our workspace:
```sh
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

At this point the workspace contains a single empty directory `src`:
```sh
.
└── src

1 directory, 0 files
```

</br>

> ***NOTE: Till here is what you need for TASK 0 to get started. Further if you want to explore more on ROS workspace, happy learning...***

---

### Add some sources

Let’s clone the [examples](https://github.com/ros2/examples) repository into the `src` directory of the workspace:
```sh
git clone https://github.com/ros2/examples src/examples -b humble
```

Now the workspace should have the source code to the ROS 2 examples:

```sh
.
└── src
    └── examples
        ├── CONTRIBUTING.md
        ├── LICENSE
        ├── rclcpp
        ├── rclpy
        └── README.md

4 directories, 3 files
```

### Source an underlay

It is important that we have sourced the environment for an existing ROS 2 installation that will provide our workspace with the necessary build dependencies for the example packages. This is achieved by sourcing the setup script provided by a binary installation or a source installation, ie. another colcon workspace (see [Installation](https://docs.ros.org/en/humble/Installation.html)). We call this environment an **underlay**.

### Build the workspace

In the root of the workspace, run `colcon build`. Since build types such as `ament_cmake` do not support the concept of the `devel` space and require the package to be installed, colcon supports the option `--symlink-install`. This allows the installed files to be changed by changing the files in the `source` space (e.g. Python files or other non-compiled resources) for faster iteration.

```sh
colcon build --symlink-install
```

After the build is finished, we should see the `build`, `install`, and `log` directories:

```sh
.
├── build
├── install
├── log
└── src

4 directories, 0 files
```

### Run tests (Optional)

To run tests for the packages we just built, run the following:

```sh
colcon test
```

> ***NOTE: This may fail sometimes due to non-updated packages. You may ignore this command and no need to run `colcon test` if your `colcon build` has ran successfully.***

### Source the environment

When colcon has completed building successfully, the output will be in the `install` directory. Before you can use any of the installed executables or libraries, you will need to add them to your path and library paths. colcon will have generated bash/bat files in the `install` directory to help set up the environment. These files will add all of the required elements to your path and library paths as well as provide any bash or shell commands exported by packages.

```sh
source install/setup.bash
```


## Create your own package:

colcon uses the `package.xml` specification defined in [REP 149](https://www.ros.org/reps/rep-0149.html) ([format](https://www.ros.org/reps/rep-0140.html) 2 is also supported).

colcon supports multiple build types. The recommended build types are `ament_cmake` and `ament_python`. Also supported are pure `cmake` packages.

An example of an `ament_python` build is the [ament_index_python package](https://github.com/ament/ament_index/tree/humble/ament_index_python) , where the *setup.py* is the primary entry point for building.

A package such as [demo_nodes_cpp](https://github.com/ros2/demos/tree/humble/demo_nodes_cpp) uses the `ament_cmake` build type, and uses CMake as the build tool.

For convenience, you can use the tool `ros2 pkg create` to create a new package based on a template.


## Setup `colcon_cd`:

The command `colcon_cd` allows you to quickly change the current working directory of your shell to the directory of a package. As an example `colcon_cd some_ros_package` would quickly bring you to the directory `~/ros2_ws/src/some_ros_package`.

```sh
echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
echo "export _colcon_cd_root=/opt/ros/humble/" >> ~/.bashrc
```

Depending on the way you installed `colcon_cd` and where your workspace is, the instructions above may vary, please refer to the [documentation](https://colcon.readthedocs.io/en/released/user/installation.html#quick-directory-changes) for more details. To undo this in Linux and macOS, locate your system’s shell startup script and remove the appended source and export commands.


## Tips:

- If you do not want to build a specific package place an empty file named `COLCON_IGNORE` in the directory and it will not be indexed.

- If you want to avoid configuring and building tests in CMake packages you can pass: `--cmake-args -DBUILD_TESTING=0`.

- If you want to run a single particular test from a package:
    ```sh
    colcon test --packages-select YOUR_PKG_NAME --ctest-args -R YOUR_TEST_IN_PKG
    ```


## References:

- [Configuring ROS 2 Environment](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Configuring-ROS2-Environment.html)

- [Creating a ROS 2 Workspace](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace.html)

</br>

---