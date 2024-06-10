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
    <h1>Task 1A - Submission</h1>
</center>

---

## Submission instructions for task 1A:

> * ***NOTE:** All your tasks will be checked using a plagiarism software. If any submitted file is found to be plagiarised, e-Yantra reserves the right to disqualify the team.*

1. Upgrade your `eyantra-autoeval` package by running the command given below

    ```sh
    pip3 install -U eyantra-autoeval
    ```

2. First launch the robot in gazebo as instructed before `ros2 launch ur_description ur5_gazebo_launch.py` and `ros2 launch ur5_moveit spawn_ur5_launch_moveit.py` keep it running. Also, run your Task 1A python script in a new terminal.

3. Then open another terminal and execute the auto eval script `eyantra-autoeval evaluate --year 2023 --theme CL --task 1A`.

4. Make sure you execute above auto eval command once you are able to see TF for package box `[obj_1, obj_3 and obj_49]` in RViz to successfully record a bag file.

5. The auto eval script will record data by creating a `my_bag/my_bag_0.db3` bag file in the same directory *(inside a folder named `my_bag`)* for around 5 seconds and then close automatically. 
   - Once you see this message from auto eval script `-> Data collection completed! Thankyou for being patient ;) Follow instructions on portal mdbook to submit task 1A.` you can terminate your launch files and python script. 
   - This would be considered as a successfull submission for Task 1A. (marks are yet to be evaluated...)
   - Also, a `metadata.yaml` will be generated along with the bag file. Make sure you zip this file too.

6. NOTE: Do take a screenshot of the cv2 window having aruco tag borders drawing and object pose axis representation markings as shown in [Expected output -> Image Window (color window)-](./instructions.md) image and submit the same by adding the image file in the below mentioned directory which will be zipped and submitted. **(Rename the image filename as `CL#<team_id>_color_image`. For ex: `CL#1967_color_image.png`)**

7. Now add your python script to the same directory (along with the screenshot; refer point [6] above) and create a `.zip` file by selecting only these four files **i.e. Python, Image Screenshot, Bag file and Metadata file** . Take a look at the below `.GIF` to understand it better. (Note: Do not compress the whole folder)


8. Once the zip is created, rename it as `<CL#team_id_1A>` *(For example, if your team id is 1679, rename file as `CL#1967_1A.zip`)* and submit on **eYRC Portal - Task 1** by selecting option 1A.

<iframe width="700" height="400"
    src="https://www.youtube.com/embed/R0utItoBn9o?si=Phj_hdfbgKSK6foT">
</iframe> 

---

### Grading 

> **This task will be graded out of 35**
>  
>   `Successful Task` - `Marks: 35.00` <br>
>   `Failed Task` - `Marks: 0.00`

### Formula

> ***Task 1A Marks = (CAP * 5) + (CAA * 5) + (AIP * 5)***

**CAP: Correct Aruco-Marker Position** -
- The position corresponds to tf published for each individual object w.r.t. base_link
- Its is the difference between package box original pose and tf pose published by you
- Detecting each box consists of **5 marks** (In all 15 marks for all three boxes)
- Allowed position tolerance: +/- 0.15 (in meter)
- CAP = Successfull number of Aruco-Marker position found in TF (Maximum count = 3)

**CAA: Correct Aruco-Marker Angle** -
- The angle corresponds to tf published for each individual object w.r.t. base_link
- Its is the difference between package box original angle and tf angle published by you
- Detecting each box consists of **5 marks** (In all 15 marks for all three boxes)
- Allowed angular tolerance: +/- 0.174533 rad (or 10 degrees)
- CAA = Successfull number of Aruco-Marker angle found in TF (Maximum count = 3)

**AIP: Incorrect Aruco Detection** -
- This is in correspondance to avoid packages which are away from robot arm reach position
- This also includes packages which are duplicate and away from robot arm reach position (If any duplicate packages found, only consider the one which is in reach of robot arm and ignore others)
- On successfull avoidance of above mentioned cases, one will receive **5 marks** for the same.
- Allowed boxes: Only three boxes on rack
AIP = If incorrect aruco-markers detected, then you'll receive 0. Else, 1

---