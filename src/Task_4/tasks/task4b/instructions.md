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
    <h1>Welcome to Task 4B</h1>
</center>

---

</br>


### 4B **Pick and place package using UR5 Arm**

In this task team have to connect to the hardware, pick the package box from the rack and place it on the drop location.

- Make sure to take note of the follwing:
	- Make sure to **comment** out the module `linkattacher_msgs.msg` call for `AttachLink`.
	- Service for gripper changes from `/GripperMagnetON` and `/GripperMagnetOFF` to `/io_and_status_controller/set_io` with states in service call. The service function works like (team can use this function):

	```python
	from ur_msgs.srv import SetIO
	def gripper_call(self, state):
        '''
        based on the state given as i/p the service is called to activate/deactivate
        pin 16 of TCP in UR5
        i/p: node, state of pin:Bool
        o/p or return: response from service call
        '''
        gripper_control = self.create_client(SetIO, '/io_and_status_controller/set_io')
        while not gripper_control.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('EEF Tool service not available, waiting again...')
        req         = SetIO.Request()
        req.fun     = 1
        req.pin     = 16
        req.state   = float(state)
        gripper_control.call_async(req)
        return state
	```

	- When interchanging servo controller to trajectory controller or vice-versa, make sure to use the following:

	```python
	from controller_manager_msgs.srv import SwitchController # module call

	######## Use this inside the class init #######
	self.__contolMSwitch = self.create_client(SwitchController, "/controller_manager/switch_controller")
	################################################

	
	######## Use this part of the code to switch between servo and joint trajectory mode #########################
	# Parameters to switch controller
	switchParam = SwitchController.Request()
	switchParam.activate_controllers = ["scaled_joint_trajectory_controller"] # for normal use of moveit
	switchParam.deactivate_controllers = ["forward_position_controller"] # for servoing
	switchParam.strictness = 2
	switchParam.start_asap = False

	# calling control manager service after checking its availability
	while not self.__contolMSwitch.wait_for_service(timeout_sec=5.0):
		self.get_logger().warn(f"Service control Manager is not yet available...")
	self.__contolMSwitch.call_async(switchParam)
	print("[CM]: Switching Complete")
	#################################################################################################################

	```

	- Interchange the `switchParam.activate_controllers` and `switchParam.deactivate_controllers` depending on the use case within your algorithm.
	- Make sure to add pre and post pick position for efficient pick and place of the package box.

	- Note the joint-angles for the following, (if anyone wish to know the pose, find the forward kinematics of the same):
		- **Home Angles:** [0, -2.398, 2.43, -3.15, -1.58, 3.15]
		- **Drop Angles:** [-0.027, -1.803, -1.3658, -3.039, -1.52, 3.15]


### Arena Setup and rules

- There will be two boxes kept on two racks in front of the camera (one on front and other on side).
- First try to pick the box on front and then proceed to pick the one on side.
- **Make sure you have a backup internet connection along with your primary internet setup (prefereably keep two different SIM operator as backup, if you are using mobile hotspot)**
- All the TFs of two boxes should be present at an instant to avail maximum marks, OR the instant at which maximum number of detected TF are present is considered as your maximum detected count of TFs.
- Once detected, team can proceed to pick and place those boxes from the rack onto the table.
- Both boxes needs to be picked and placed in one run to avail the maximum count of parameters.

### Formula

> **Total_Marks** = (3 * ACI) + (7 * ACP) + (7 * ACD) + (Bonus)

**Note:**
- **ACI:** Arm Correct Identification: Count of TF with respect to Base Link. (max value: 2)
- **ACP:** Arm Correct Pick: Count of packages correctly picked from the rack. (max value: 2)
- **ACD:** Arm Correct Drop: Count of packages dropped correctly on the drop location. (max value: 2)

- Repeated publishing of TF of a same aruco won't increase the ACI value.
- **B:** Bonus marks which will be awarded if a team is having maximum value of ACI, ACP and ACD as 2. (max value: 1 (binary))

<p></p>

</br>

---
