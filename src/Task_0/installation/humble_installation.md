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
    <h1>ROS 2 Humble Installation Guide</h1>
</center>

---

</br>

*(This Document assumes that the reader has installed Ubuntu 22.04. However, if you haven’t installed Ubuntu 22.04 yet make sure to install it before proceeding.)*


> * ***Please practise and execute all the content related to this eYRC theme in Ubuntu 22.04 only. Developers of this theme have tested all the provided material/packages only on the mentioned Operating system.***
>
> * ***e-Yantra won’t be able to help solve queries related to any other Operating System.***


## Installation Instructions

_ROS (Robot Operating System) provides libraries and tools to help software developers create robot applications. It provides hardware abstraction, device drivers, libraries, visualisers, message-passing, package management, and more. ROS is licensed under an open source, BSD license._

***(You can refer to the [official installation guide](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html) from ROS documentation.)***

Here the [distribution](https://docs.ros.org/en/rolling/Releases.html) compatible with Ubuntu 22.04 is the [ROS Humble Hawksbill](http://docs.ros.org/en/humble/). Follow the steps below to install it.


### Installation Steps

**1. Set locale:** Make sure you have a locale which supports “UTF-8”. For this try the following commands
    
    locale  # check for UTF-8

    sudo apt update && sudo apt install locales
    sudo locale-gen en_US en_US.UTF-8
    sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
    export LANG=en_US.UTF-8
    
    locale  # verify settings
    

**2. Setup Sources:** You will need to add the ROS 2 apt repository to your system. *(More about **curl** [here](https://curl.se/))*
- First ensure that the [Ubuntu Universe repository](https://help.ubuntu.com/community/Repositories/Ubuntu) is enabled.
    ```
    sudo apt install software-properties-common
    sudo add-apt-repository universe
    ```
- Now add the ROS 2 GPG key with apt.
    ```
    sudo apt update && sudo apt install curl -y
    sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
    ```
- Then add the repository to your sources list.
    ```
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
    ```

**3. Install ROS 2 packages:** 
- Update your apt repository caches after setting up the repositories.
    ```
    sudo apt update
    ```
- ROS 2 packages are built on frequently updated Ubuntu systems. It is always recommended that you ensure your system is up to date before installing new packages.
    ```
    sudo apt upgrade
    ```
- ***Desktop Install (Recommended):*** ROS, RViz, demos, tutorials.
*(Make sure you install **Desktop** and not *ROS-Base* or *Development tools*, as we will be using *RViz* and other softwares/packages which come pre-installed in Desktop installation.)*
    ```
    sudo apt install ros-humble-desktop
    ```

**4. Environment Setup:**
- Set up your environment by sourcing the following file.
    ```
    source /opt/ros/humble/setup.bash
    ```
- To Automatically add ROS environment variables to your bash session every time a new shell terminal/bash is launched, enter the following command. *(Find more about bash [here](https://www.gnu.org/software/bash/manual/html_node/What-is-Bash_003f.html))*
    ```
    echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
    ```
- Sourcing bashrc ensures to use updated bashrc using the following command, *or* it can be done by closing all terminals and re-opening a new terminal.
    ```
    source ~/.bashrc
    ```

### Check installation
Run the below command on a new terminal after performing all the steps above, this will ensure that the ROS installed on your system is working fine.

In one terminal, source the setup file and then run a C++ ***talker***:
```
ros2 run demo_nodes_cpp talker
```

In another terminal source the setup file and then run a Python ***listener***:
```
ros2 run demo_nodes_py listener
```

You should see the ***talker*** saying that it’s ***publishing*** messages and the ***listener*** saying ***I heard*** those messages. This verifies both the *C++* and *Python APIs* are working properly. 

<p></br><b><i>Hooray! This confirms that ROS Humble has been installed successfully in your system and is running perfectly.</i></b></p>

</br>

---

### References

* [Official ROS2 Humble Documentation](https://docs.ros.org/en/humble/index.html)
* [ROS Humble Installation Instructions for Ubuntu](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html)

</br>

---