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
    <h1>Task 1B - Instructions</h1>
</center>

---

### Task:

> **Note:** Before attempting the task make sure you have gone through the [learning resources - manipulation of robotic arm](../../learning_resources/arm_manipulation/arm_manipulation.md).

> **HINT:** It will be handy for you, if you have gone through the  learning resources before starting this task. Checkout spawning of UR5 in [control ur5 arm page](../../learning_resources/arm_manipulation/moveit/control_ur5.md).

- You have to write a **single** Python script and start the same to move the arm in the order of: 
**P1 &rarr; D &rarr; P2 &rarr; D**
where position (of `tool0` in [x, y, z] format with respect to `base_link`): 
	- **P1 (Pick position 1 - front box):** &nbsp; [0.35, 0.1, 0.68]
	- **P2 (Pick position 2 - right box):** &nbsp; [0.194, -0.43, 0.701]
	- **D  (Drop position) &emsp; &emsp; &emsp; &emsp; &ensp; :** &nbsp; [-0.37, 0.12, 0.397] 

- You may watch the expected output video recording to clear out any confusion. The arm movement to drop position should be after a pick position, to be considered as valid drop position reach in the submission.

> **Note:** 
> - Your arm movement can be different as you might be using different algorithm or method for the same. 
> - You are free to use the `servoing` method **OR** let moveit plan (i.e. actuate directly by giving pose or joint angles using `move_group` action) **OR** combination of both.

> ***HINT:** You are also free to add any intermediate pose to achieve the completion of this task.*

---

### Getting Started

- Use `ur5_gazebo_launch.py` launch file of `ur_description` package to start gazebo waiting for ur5 spawn.
- Now, start the launch file which you have made during `moveit_setup_assistant` i.e. `spawn_ur5_launch_moveit.launch.py` to spawn arm in gazebo as well as in RVIZ to control it using `Moveit Planning Interface` plugin of Rviz.

---

### Expected Output
You can compare the execution of your python file with UR5 in Gazebo: *(Your implementation may look different, as the main aim is to reach the desired given points)*

(*It might take some time to load the video ;p*)

<!-- <video width="600" height="500" controls> 
  <source src="cut1b.mp4" type="video/mp4">
</video> -->
<iframe width="700" height="400"
    src="https://www.youtube.com/embed/DNCeV9lVZUQ?si=05gGEgWEH3AYPltt">
</iframe> 

---

> **Note:** Deadline for the submission of this task is **16th October, 2023**