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
    <h1>Welcome to Task 5</h1>
</center>

---

</br>


### Task - **Dock, Pick and Place multiple boxes**
*Dock the rack using ebot towards robot arm and pick and place in dropbox*

> **NOTE:** You will be provided with the same workspace where you left off in task 4. If any team requires a fresh start, are free to do so in the same workspace. This time this single workspace will include all of your eBot and Arm packages.

#### Task
- In this task you have to bring two racks present in the arena towards UR5 arm and need to pick/drop 3 boxes.

- One Rack with a box will be present on right hand side of UR5 arm, while other two are required to bring by eBot.

- Start eBot navigation bringup launch using `ros2 launch ebot_real_nav2 ebot_nav2_brinup.launch.py` command. 

- If a team is using `imu fusion (ekf filtering)` then make sure you also run the imu duplication node using `ros2 run ebot_control duplicate_imu` command.

- Make sure you reset odometry using `reset_odom` service whenever you start from home position for better performance.

- You may use imu reset service to `reset_imu` when you feel/observe the imu values are varying too much. It is individuals call when to reset this.

- (Not recommended) To reset arduino, you may use `usb_relay_sw` service with `relay channel = 0` (for explanation, refer to accessories section of [task 4A documentation](../Task_4/tasks/task4a/instruction.md))

- Navigate to the specified rack having the package mentioned in the configuration file as `package_id`. You can use the `yaml` python module to read the values.
<a href="./config.yaml"  target="blank"><button type="button">Download</button></a>

    - (If the above link doesn't work, try to copy the content given below to a file named `config.yaml`, which should be created by you)

        ```yaml
        position:
            - rack1: [6.5, 0.75, 1.57]
            - rack2: [1.15, -2.2, 0.0]
            - rack3: [0.5, 2.05, 0.0]
            - arm: [6.3, -0.05, 3.14]

        package_id: [3, 2, 1]
        ```

    - Dock and bring the rack in front of the arm.

    - Find the TF of the aruco marker, and finally do manipulation of the robotic arm.

    - The arm should be able to pick the box from the rack and place it on the drop position (i.e. table kept behind the arm).

    - This is to be repeated for second rack

### Explicit Rules for task 5:

- Once you start the task, no starting or stopping of any scripts are allowed during the run.
    - You can create your launch files and scripts if required, you are free to use your workspace.
    - Also, the navigationa, docking, robot footprint updates, service call for docking completion and start arm pick, etc. everything should be in one go as performed in task 4C.
- You may use service calls or topic callbacks to communicate between eBot and Arm task completion status. 
    - You are free to use any method for communication.
- You cannot start the eBot apart from home position for navigation (during the final evaluation, meanwhile can use any pose for testing).
- ECD, eBot correct drop points will be considered only when eBot drops rack in correct pose, detaches itself from rack by turning off the magnet and move ahead with come clearance.

</br>

---
