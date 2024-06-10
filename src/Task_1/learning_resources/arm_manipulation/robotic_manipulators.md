# Robotic Manipulators / Robotic Arms

* These are robots designed to manipulate the environment around them.
* These are commonly referred to as Robotic Arms.

![turtle](https://raw.githubusercontent.com/erts-RnD/krishiBot_images/main/man1.png)

<p>Image from <a href="http://wiki.ros.org/Books/ROS_Robot_Programming_English">ROS Robot Programming Book</a> </p>
</center>


* This is a typical structure of a manipulator. A manipulator consists of Joints, Links, an End effector, and a base.
  
  * **Joints**: These are the movable components of a robotic arm. Joints allow the movement of links. Actuators like motors allow the movement of joints.
  
  * **Links**: These are rigid structures used to connect joints. Movement of links is possible with joints only.
  
  * **End-Effector**: In serial robotic manipulators, the end effector means the last link of the robot. An end effector is a device at the end of a robotic arm, designed to interact with the environment. For example, the mechanism gives the gripping capability to a robotic arm.
  
  * **Base**: It is a plane to which a robotic arm is connected.
  
    
  
* A robotic arm is very similar to a human arm.
  * Your elbow and wrist are similar to joints.
  * Your forearm is like a link that connects two joints i.e your elbow and wrist.
  * Your palm and fingers are the end-effectors.
  * Your torso is the base for your arm.

<center><img src="https://openoregon.pressbooks.pub/app/uploads/sites/42/2018/07/Elbow-Angle-300x268.jpg" style="scale:100%;" />
<p>Image from <a href="https://openoregon.pressbooks.pub/bodyphysics/chapter/tipping-point/">Open Oregon</a> </p> </center> 



##   <span class="blink_text">Reading Assignment</span>

* Chapter-13, Manipulators, [ROS Robot Programming Book](https://discuss.e-yantra.org/t/books-for-reference/10428) [**Section 2.1**]

# Kinematics

* It is a branch of mathematics that deals with the motion of a body or system of bodies.
* It describes the motion of points, bodies, or systems of bodies without looking into forces that cause them to move.
* Before diving deep let's look at why we need kinematics in the first place?



## Why Kinematics?

<center><img src="https://raw.githubusercontent.com/souravjena/vb_assets/master/home/download.jpeg" style="scale:100%;" /> 
<p>Image from <a href="https://www.researchgate.net/figure/We-use-a-UR5-robotic-arm-to-define-reinforcement-learning-tasks-based-on-two-joints_fig1_323867754">Researchgate</a> </p>
</center>

* Suppose you have a robotic arm and you want to pick a box using this arm.
* You know the position of the box in Cartesian space i.e you know the x, y, and z of the box in space.
* Now in order to pick this box you need the end-effector of your robotic arm to go near the box and then pick it.
* To make this possible you need to actuate the joints of your robotic arm in such a way that the end-effector is able to reach the box.
* Now, how much do you need to actuate each joint for this? This is an **Inverse Kinematics** problem.
* Given the position of the end-effector in Cartesian space you can calculate the angle of rotation for each joint using Inverse Kinematics.
* If you have joint angles and you need to calculate the position of your end-effector in Cartesian space you can calculate that using **Forward Kinematics**.


<center><img src="https://www.researchgate.net/publication/319127421/figure/fig1/AS:631651373686833@1527608831926/Relationship-between-forward-and-inverse-kinematics.png" style="scale:100%;" /> 
<p>Image from <a href="https://www.researchgate.net/figure/We-use-a-UR5-robotic-arm-to-define-reinforcement-learning-tasks-based-on-two-joints_fig1_323867754">Researchgate</a> </p>
</center>


-------------
<div data-theme-toc="true"> </div>