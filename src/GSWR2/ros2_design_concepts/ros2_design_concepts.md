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
    <h1>ROS2 Design Concepts</h1>
</center>

---

</br>

*In this module we will cover the introduction to ROS, it's history, difference between ROS1 and ROS2, what is DDS, ROS2 design concepts, etc.*

> **[1. History of ROS](history_of_ros.md)**
- **Early Beginnings**
  - Origin of ROS (Robot Operating System)
  - The initial purpose and goals of ROS
  - Key milestones in ROS development
- **Evolution to ROS2**
  - The need for ROS2: Limitations of ROS1
  - Introduction to ROS2 development
  - Community involvement and contributions

> **[2. Differences between ROS1 and ROS2](diff_ros_1_and_2.md)**
- **Architecture**
  - Comparison of the underlying architecture
  - Middleware: ROS1's custom middleware vs. ROS2's DDS
- **Communication**
  - Differences in communication paradigms
  - Improvements in inter-process and inter-node communication
- **Performance and Reliability**
  - Enhanced real-time capabilities
  - Quality of Service (QoS) policies in ROS2
- **Security**
  - Security enhancements in ROS2
  - Secure communication features
- **Compatibility and Portability**
  - Cross-platform support (Windows, Linux, macOS)
  - Mobile and embedded system compatibility
- **Development and Deployment**
  - Differences in development tools and processes
  - Improvements in deployment and lifecycle management

> **[3. Data Distribution Service (DDS)](dds.md)**
- **What is DDS?**
  - Introduction to DDS
  - Key features and capabilities of DDS
- **Role of DDS in ROS2**
  - How DDS integrates with ROS2
  - Benefits of using DDS in ROS2
  - Examples of DDS implementations used in ROS2 (e.g., FastDDS, CycloneDDS)
- **DDS Concepts**
  - Overview of DDS concepts: Topics, Data Writers, Data Readers, QoS policies
  - Real-time data distribution and communication
  - Scalability and flexibility in distributed systems

> **4. ROS2 Design Concepts**
- **Nodes and Components**
  - Definition and role of nodes in ROS2
  - Composition and lifecycle of nodes
  - Nodelets and intra-process communication
- **Topics, Services, and Actions**
  - Communication mechanisms: Topics, Services, Actions
  - Use cases and examples of each mechanism
  - QoS policies and their impact on communication
- **Parameter Server**
  - Role and usage of the parameter server
  - Dynamic reconfiguration of parameters
- **Launch System**
  - Overview of the launch system in ROS2
  - Launch files and their syntax
  - Examples of launching ROS2 nodes and systems
- **Lifecycle Management**
  - Node lifecycle states and transitions
  - Managed nodes and their benefits
- **Component-Based Architecture**
  - Introduction to component-based design
  - Benefits of using components for modular development
  - Examples of component-based architectures in ROS2
- **Interoperability and Integration**
  - Integration with other systems and frameworks
  - Interoperability with ROS1 (ROS1-ROS2 bridge)

> **5. Conclusion**
- **Summary**
  - Recap of key points covered in the module
- **Further Reading and Resources**
  - Recommended resources for deeper understanding
  - Community forums and discussion groups

</br>

-------