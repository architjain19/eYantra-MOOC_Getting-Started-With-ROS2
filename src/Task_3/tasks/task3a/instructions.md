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
    <h1>Welcome to Task 3</h1>
</center>

---

</br>


### 3A **Aruco and TF on Hardware**

In this task team have to connect to the hardware and publish TF of aruco marker detected using the resources given in the `anydesk` and `husarnet` section in your respective slot. For more understanding of how slot and hardware connection works, kindly refer the video instruction given in the same section.

- **Step 1:** Connect to the remote hardware using `anydesk` (recommended) or `husarnet` (can be used for debugging) keeping your github repository ready, along with joining Google meet link given in the Google Sheet (link will be provided in the discuss forum).

- **Step 2:** Run your script to detect the aruco marker given on the topic `/camera/color/image_raw`, you may also choose to use the compressed topic, but make sure your function is ready to receive the same. For depth you can use `/camera/aligned_depth_to_color/image_raw` topic. Also, make sure to cross-check with `camera parameters` using the camera info topic.

- **Step 3:** Publish the TF using the naming convention `<team_id>_cam_<aruco_id>` for TF with respect to camera_link. For publishing TF with respect to `base_link` use the naming convention as `<team_id>_base_<aruco_id>`.

### Arena Setup and rules

- There will be three boxes kept on two racks in front of the camera.
- The boxes can be kept in any order (in any fashion).
- **Make sure you have a backup internet connection along with your primary internet setup (prefereably keep two different SIM operator as backup, if you are using mobile hotspot)**
- All the TFs of three boxes should be present at an instant to avail maximum marks, OR the instant at which maximum number of detected TF are present is considered as your maximum detected count of TFs.

### Formula

> Total_Marks = (5 * CCL) + (10 * CBL) + (5 * B)

**Note:**
- **CCL:** Count of TF with respect to Camera Link (max value: 3)
- **CBL:** Count of TF with respect to Base Link (max value: 3)
- Repeated publishing of TF of a same aruco won't increase the CCL or CBL value.
- **B:** Bonus marks which will be awarded if a team is having maximum value CCL and CBL as 3. (max value: 1 (binary))

<p></p>

</br>

---
