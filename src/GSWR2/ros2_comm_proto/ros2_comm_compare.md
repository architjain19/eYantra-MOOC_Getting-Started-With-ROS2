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
    <h1>Comparing Topics, Services, and Actions in ROS2</h1>
</center>

---

### Introduction

> In the ROS2 ecosystem, communication between nodes is facilitated through three primary mechanisms: Topics, Services, and Actions. Each of these communication paradigms serves distinct purposes and is suited for different use case scenarios. Understanding when to use each mechanism is crucial for building efficient and effective robotic applications.

### Use Case Scenarios

#### When to Use Topics

**Topics** are used for continuous, asynchronous data streaming. They are ideal for scenarios where data needs to be published at a regular rate and multiple subscribers may be interested in the data.

**Common Use Cases**:
- **Sensor Data Streaming**: For example, a camera node publishing image data or a LiDAR node publishing point cloud data.
- **Telemetry and Status Updates**: Nodes publishing their status or telemetry data, such as battery levels or robot position.
- **Control Commands**: Sending high-frequency control commands to actuators or motors.

**Example**:
> A LiDAR sensor node publishes a point cloud data stream on the /lidar_points topic, and multiple nodes subscribe to this topic to process the data for mapping, obstacle detection, and navigation.

#### When to Use Services

**Services** are used for synchronous, request-response interactions. They are suited for scenarios where a node needs to request a specific operation and wait for the result.

**Common Use Cases**:
- **Configuration Changes**: Requesting a change in the configuration of a node, such as changing a parameter or mode of operation.
- **Specific Queries**: Requesting specific data or performing a computation that does not need to happen continuously.
- **Triggering Actions**: Performing discrete actions that require confirmation, such as opening a gripper or starting a recording.

**Example**:
A client node sends a request to a service server to add two integers. The server processes the request and returns the result to the client.

#### When to Use Actions

**Actions** are used for long-running tasks that require feedback and can be preempted. They are suitable for operations that take a considerable amount of time and where progress updates or the ability to cancel the task is necessary.

**Common Use Cases**:
- **Navigation Tasks**: Moving a robot to a specified location with feedback on the progress and the ability to cancel the task if needed.
- **Manipulation Tasks**: Performing complex manipulations such as picking and placing objects where intermediate feedback and the ability to preempt the task are essential.
- **Data Processing Tasks**: Long-running data processing tasks that can provide updates on progress and can be stopped if required.

**Example**:
A navigation action server receives a goal to move the robot to a specified location. The server provides continuous feedback on the robot's position and allows the client to cancel the goal if necessary.

### Comparative Analysis

#### Latency

- **Topics**: Generally low latency due to the asynchronous nature of message passing. Suitable for high-frequency data streams.
- **Services**: Latency depends on the request-processing time. It can be higher than topics because the client waits for the server's response.
- **Actions**: Latency includes both the initial request and the ongoing feedback. While initial communication might have latency similar to services, the continuous feedback loop can introduce additional delays.

#### Reliability

- **Topics**: Reliability can be affected by network conditions. QoS (Quality of Service) settings can be configured to improve reliability, such as setting up reliable or best-effort delivery.
- **Services**: More reliable for individual transactions as the client waits for a response. However, it might suffer from higher latency if the server is busy or the request is complex.
- **Actions**: Designed to handle long-running tasks with feedback and preemption, making them inherently more complex but reliable for tasks that require monitoring and potential cancellation.

#### Complexity

- **Topics**: Simplest form of communication in ROS2. Easy to set up and use for streaming data.
- **Services**: Moderately complex due to the need for request-response handling. Suitable for discrete tasks requiring confirmation.
- **Actions**: Most complex due to the requirement for feedback and preemption mechanisms. Ideal for long-running tasks that need monitoring and control.

### Conclusion

> Choosing between Topics, Services, and Actions in ROS2 depends on the specific requirements of your application. Topics are ideal for continuous data streaming with low latency needs. Services are suitable for synchronous request-response interactions where reliability for discrete tasks is important. Actions are the best choice for long-running tasks that require feedback and the ability to be preempted. By understanding the strengths and weaknesses of each communication mechanism, you can design more efficient and robust robotic systems.

-------