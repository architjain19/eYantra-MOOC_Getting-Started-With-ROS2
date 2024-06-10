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
    <h1>ROS 2 Package</h1>
</center>

---

</br>

This tutorial will teach you how to create your first ROS 2 application. It is intended for developers who want to learn how to create custom packages in ROS 2, not for people who want to use ROS 2 with its existing packages.

## Creating a package:

All ROS 2 packages begin by running the command

```sh
ros2 pkg create <pkg-name> --dependencies [deps]
```

in your workspace (usually `~/ros2_ws/src`).

</br>

To create a package for a specific client library:

- For C++:
    ```sh
    ros2 pkg create <pkg-name> --dependencies [deps] --build-type ament_cmake
    ```
- For Python:
    ```sh
    ros2 pkg create <pkg-name> --dependencies [deps] --build-type ament_python
    ```

You can then update the `package.xml` with your package info such as dependencies, descriptions, and authorship.

### C++ Packages

You will mostly use the `add_executable()` CMake macro along with

```sh
ament_target_dependencies(<executable-name> [dependencies])
```
to create executable nodes and link dependencies.

To install your launch files and nodes, you can use the `install()` macro placed towards the end of the file but before the `ament_package()` macro.

An example for launch files and nodes:

```sh
# Install launch files
install(
  DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)

# Install nodes
install(
  TARGETS [node-names]
  DESTINATION lib/${PROJECT_NAME}
)
```

### Python Packages

ROS 2 follows Python’s standard module distribution process that uses `setuptools`. For Python packages, the `setup.py` file complements a C++ package’s `CMakeLists.txt`. More details on distribution can be found in the [official documentation](https://docs.python.org/3/distributing/index.html#distributing-index).

In your ROS 2 package, you should have a `setup.cfg` file which looks like:

```sh
[develop]
script_dir=$base/lib/<package-name>
[install]
install_scripts=$base/lib/<package-name>
```

and a `setup.py` file that looks like:

```sh
import os
from glob import glob
from setuptools import setup

package_name = 'my_package'

setup(
    name=package_name,
    version='0.0.0',
    # Packages to export
    packages=[package_name],
    # Files we want to install, specifically launch files
    data_files=[
        # Install marker file in the package index
        ('share/ament_index/resource_index/packages', ['resource/' + package_name]),
        # Include our package.xml file
        (os.path.join('share', package_name), ['package.xml']),
        # Include all launch files.
        (os.path.join('share', package_name, 'launch'), glob(os.path.join('launch', '*.launch.py'))),
    ],
    # This is important as well
    install_requires=['setuptools'],
    zip_safe=True,
    author='ROS 2 Developer',
    author_email='ros2@ros.com',
    maintainer='ROS 2 Developer',
    maintainer_email='ros2@ros.com',
    keywords=['foo', 'bar'],
    classifiers=[
        'Intended Audience :: Developers',
        'License :: TODO',
        'Programming Language :: Python',
        'Topic :: Software Development',
    ],
    description='My awesome package.',
    license='TODO',
    # Like the CMakeLists add_executable macro, you can add your python
    # scripts here.
    entry_points={
        'console_scripts': [
            'my_script = my_package.my_script:main'
        ],
    },
)
```

### Combined C++ and Python Packages
When writing a package with both C++ and Python code, the `setup.py` file and `setup.cfg` file are not used. Instead, use [ament_cmake_python](https://docs.ros.org/en/humble/How-To-Guides/Ament-CMake-Python-Documentation.html).


## References:

- [Developing a ROS 2 Package](https://docs.ros.org/en/humble/How-To-Guides/Developing-a-ROS-2-Package.html)

</br>

---