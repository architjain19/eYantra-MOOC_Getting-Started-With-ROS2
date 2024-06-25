# Launch files and running ROS nodes

> **Launch files**
The launch system in ROS 2 is responsible for helping the user describe the configuration of their system and then execute it as described. The configuration of the system includes what programs to run, where to run them, what arguments to pass them, and ROS-specific conventions which make it easy to reuse components throughout the system by giving them each a different configuration. It is also responsible for monitoring the state of the processes launched, and reporting and/or reacting to changes in the state of those processes. 
Launch files are written in Python, XML, or YAML can start and stop different nodes as well as trigger and act on various events.

 - **[1. Key Components of Launch Files](2_launch_files.md)**
    - Basic Structure
    - Including Other Launch Files
    - Setting Parameters
    - Remapping Topics
    - Arguments
    - Groups

 - **[2. Creating Launch File for Publisher and Subscriber nodes](2_1_launchfile_pubsub.md)**
