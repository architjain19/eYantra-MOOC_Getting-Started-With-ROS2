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

<center>
    <h1>Key Concepts of ROS2</h1>
</center>

---

### *Understanding Key Concepts in ROS2*

> *In the Robot Operating System (ROS), nodes, topics, and messages are fundamental to how a distributed robotic system operates and communicates. These concepts are at the core of ROS’s decentralized architecture, allowing multiple processes (nodes) to work together by sharing data in real time.*

#### [1. Nodes](nodes.md)
>    - **Overview and Importance**
>       -   Nodes are individual units of computation that execute specific tasks within a robotic system.
>       -   They are modular and independent, enabling developers to decompose complex functionalities into manageable components.
>       -   Example: In a differential drive robot, separate nodes can handle navigation, obstacle avoidance, and sensor data processing allowing for efficient and organized system design.

#### [2. Topics](topics.md)
>    - **Overview and Importance**
>      - Decoupled Communication
>      - Data Distribution
>      - Topics are identified by unique names, allowing for organized and structured data flow

#### [3. Messages](messages.md)
>    - **Overview and Importance**
>      - ROS provides a set of predefined message types (e.g., integers, strings, sensor data), and developers can also define custom messages.

