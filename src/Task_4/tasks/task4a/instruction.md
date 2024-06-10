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
    <h1>Welcome to Task 4A</h1>
</center>

---

</br>


### 4A **eBot Navigation and Docking**

In this task team have to connect to the hardware and perform autonomous navigation using *nav2*. You can initially test the navigation using *RViz - Go to Goal Pose* feature to test robot accuracy and tune your navigation parameters in the initial slots and then automate go to goal pose using the script similar to one used in task 2b.

- **Step 1:** Connect to the remote hardware using `anydesk` (recommended) or `husarnet` (can be used for debugging) along with joining Google meet link given in the Slot Google Spreadsheet.

- **Step 2:** Run your script to navigate the ebot from home position to pre-docking position (in front side of rack). Start your docking service to perform docking operations. While docking you can use `orientation` topic provided by eBot (which is only on hardware and can help wherever required. Details about topic msg/type are shared below).

- **Step 3:** Once, the robot is closer to the rack you can turn on the magnet using a `usb_relay_sw` service (Magent on hardware is controlled using an USB relay attached on eBOT. More details are shared below). You are independent to use your logic for when to turn on the magnet (maybe before docking starts or once it reached closed to the rack).

- **Step 4:** After the rack is attached, navigate towards the UR5 and prepare for undocking. This is to verify if the rack has attached the eBot correctly and the eBot is able to navigate using the rack. Once the rack/boxes are in reach of UR5, the ebot can demagnetise (turn OFF the electromagnet) and leave the rack. (This assures a successfull completion of task 4A)


### Arena Setup and rules

- There will be two racks present in the arena having metal strips on each rack for the magnet to attach/detach the racks from eBot. The electromagnet for which to turn it on/off you can use a ros2 service `usb_relay_sw` defined by team e-Yantra (given below).

- The remote arena map will be created by team e-Yantra and this map will be placed inside the maps folder of existing package. Need not worry about this file location, it will be written in the launch file. (Although you cannot use this map in simulation as the world present in current gazebo and hardware arena setup are different.)

- The position of racks will be randomised for different tasks. And position of rack to be picked will be defined in a `config.yaml` (shared below) as used in previous tasks. You have to use this config file in your script to get the position and use it for navigation.

<!-- - You will be provided with some sensors reading available with the eBot to get help in docking. (As you will find that `/odom` topic is not that much reliable as it was ideal in simulation. You will face drift issues, due to which with the help of ultrasonic and orientation/imu you can write your docking script) -->

- During this task in hardware, topics such as odom, cmd_vel, robot description and other related topics which are necessary will be advertised on eBot end. For this task there will be 3 packages present -
    1. eBot Nav2 - This package defines the map, mapper param, nav2 param, meshes, robot description (urdf) files together.
    2. eBot Control - This package contains python/c++ scripts writen by your team to perform task 4A. You are free to use this package to add/create any other scripts or messages/service if required.
    3. usb_realy - This package defines the service message for usb relay to turn the magent ON/OFF.

- The team have to use these packages and just tune the nav2 params as per their requirements and write a script (inside `ebot control` package) for task 4A accordingly.

- Each slot will be for 60 minutes each. And each team will get 4 slots each for eBot. So, stratergise and divide your work accordingly.

- Recommended targets for each slot - (Note: It is not compulsory to follow this)
    - Slot 1: Move ebot from home position to pre-docking position (front side of a rack) defined in the config file (using python script)
        - Test Nav2/SLAM using RViz tools first and tune the navigation parameters and further continue testing with script using nav2 service.
    - Slot 2: Perform docking of ebot starting from home position (includes attachment of rack using the electromagnet)
        - Write docking script and perform docking operations such as aligning, ultrasonic linear docking, magnet testing, etc.
    - Slot 3: Move ebot with rack and drop the rack in front of the UR5
        - Use nav2 goals to navigate ebot with rack.
        - Align the rack in front of UR5 and then turn OFF the electromagnet. The rack should be aligned in such as way that the boxes on rack are in the reach of UR5 arm. (Refer rulebook)
    - Slot 4: Full task 4A testing and submission
        - Perform all above mentioned subtasks starting from home position.

- **Make sure you have a backup internet connection along with your primary internet setup (prefereably keep two different SIM operator as backup, if you are using mobile hotspot)**

> **NOTE:** Once you start the task, no starting or stopping of any scripts are allowed during the run.

### Accessories

- **USB Relay**
    To activate the service to control USB relay (Only for hardware)-
    **Note:**
    - ***relaychannel:***
        - 0 = Arduino Reset
        - 1 = Electromagnet

    - ***relaystate:***
        - 0 = Cuts of the connection
        - 1 = Turns on the connection

    > *Example: To turn the electromagnet ON*
    > ```
    > ros2 service call /usb_relay_sw usb_relay/srv/RelaySw "{relaychannel: 1, relaystate: true}"
    > ```
    > *Example: To turn the electromagnet OFF*
    > ```
    > ros2 service call /usb_relay_sw usb_relay/srv/RelaySw "{relaychannel: 1, relaystate: false}"
    > ```

    > *Example: To reset arduino, turn ON and OFF the switch with some delay. The USB relay switch is connected to reset button of arduino, so need to turn it ON for few second and then turn OFF.*
    > ```
    > ros2 service call /usb_relay_sw usb_relay/srv/RelaySw "{relaychannel: 0, relaystate: true}"
    > # Provide delay for 1 second
    > ros2 service call /usb_relay_sw usb_relay/srv/RelaySw "{relaychannel: 0, relaystate: false}"
    > ```


- **IMU Orientation**
    To provide IMU data representation on eBot hardware, we have a topic named `/orientation` of type `Float32` which publishes **Yaw** of the eBot. 
    - The range of this orientation is from `0 - 6.28` *(in radians, i.e., 0 - 360 degrees)*
    - This topic can be used if any extra verification/logic needs to be applied

- **Ultrasonic**
    There are different ultrasonic present on eBot. You can use the two ultrasonic sensors present on behind of the eBot (similar to one used in simulation tasks).
    - Topic name for ultrasonic sensor is `/ultrasonic_sensor_std_float` of type `/Float32MultiArray` which has all ultrasonic data logged in an float multi array form.
    - You can extract the two ultrasonic sensors present on 4th and 5th position in the array using the following code-
        ```
        ultra_sub = self.create_subscription(Float32MultiArray, 'ultrasonic_sensor_std_float', self.ultra_callback, 10)

        # callback for ultrasonic subscription
        def ultra_callback(self,msg):
            self.ultra_left= msg.data[4]
            self.ultra_right = msg.data[5]
        ```

- **Config file**
    - Navigate to the specified rack having the package mentioned in the configuration file as `package_id`. You can use the `yaml` python module to read the values.

    - Download the file here - <a href="./config.yaml"  target="blank"><button type="button">config.yaml</button></a>

    - If the above link doesn't work, try to copy the content given below to a file named `config.yaml`, which should be created by you
    ```yaml
    position:
        - rack1: [1.26, 4.34, 3.14]
        - rack2: [2.03, 3.3, -1.57]
        - rack3: [2.02, -8.09, 1.57]

    package_id: [3]
    ```

    > ***Note: These coordinates might change during the hardware slots. So, verify once before you join the session***


### Formula

> Total_Marks = (10 * ECN) + (10 * ECP) + (10 * ECD) + (5 * B)

**Note:**
- **ECN:** [eBot Correct Navigation] Parameter increases when the eBot is within the desired perimeter of the rack. Repeated attempts to enter into the area of the same rack will not yield to any additional marks. (max value: 1 (binary))
- **ECP:** [eBot Correct Pick] Parameter increases when the eBot has correctly docked and attached the rack with the eBot using electromagnet. If the eBot hits/collides with the rack during docking, then ECP will be considered as 0. (max value: 1 (binary))
- **ECD:** [eBot Correct Drop] Parameter increases when the eBot has correctly dropped the rack in front of the UR5 arm and is in reach position of it. (max value: 1 (binary))
- **B:** Bonus marks which will be awarded if a team is having maximum value ECL and ECD as 1. (max value: 1 (binary))

<p></p>

</br>

---
