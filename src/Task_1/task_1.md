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
    <h1>Welcome to Task 1</h1>
</center>

---

</br>

> *The aim of Task 1 is to get you ready with small chunk of codes in simulation for further full theme implementation.*

### Update your repository before you move ahead with TASK 1

- Assuming that you have already cloned [eYRC - Cosmo Logistics Repo](https://github.com/eYantra-Robotics-Competition/eYRC-2023_Cosmo_Logistic) during your Task 0. If not then you can directly clone this repo using `git clone https://github.com/eYantra-Robotics-Competition/eYRC-2023_Cosmo_Logistic.git` and move ahead with the Task 1.

- For ones who have used this repository before, and have any changes done (if you don't want to loose any changes, you can use `git status` to see if you have done any) then first stash your changes using following command-

	(***NOTE:** Navigate inside the `src` folder of your workspace, before proceeding further*)


	```sh
	git stash
	```

- Then pull the updated Task 1 commits from the repo using-
	```sh
	git pull
	git checkout tags/v1.1.1 . # if doesn't work try `git fetch` and try again
	```

- And again pop your changes you've made before from stash using-
	```sh
	git stash pop
	```

> **Note** :  
> - For ones who haven't changed any file, can directly run `git pull` and continue. 

For directly starting with Task 1A

```sh
sudo apt-get install ros-humble-joint-state-broadcaster ros-humble-joint-trajectory-controller ros-humble-controller-manager
```
> - Do `colcon build` to build the workspace with updated packages.
>
> - NOTE: After any changes in any files, to reflect the same on workspace you need to do `colcon build`
>
> - If you want to skip this step of building every time a file (python script) is changed (note: this doesn't include addition of file or addition of folder), you may use the `colcon build --symlink-install` parameter with the build command. (Surf over the internet to find more about it)


---


### This task is divided into *three* parts:

### 1A [**Object Pose Estimation**](tasks/task1a/task1a.md)
*Locating Aruco in the world with respect to arm*


### 1B [**Arm Manipulation using Moveit**](tasks/task1b/task1b.md)
*Manipulating Robotic Arm using Moveit framework*


### 1C [**Autonomous Navigation using Nav2**](tasks/task1c/task1c.md)
*Navigating eBot in gazebo environment using Nav2*

### [**Learning Resources for Task 1**](learning_resources/learning_resources.md)

<p></p>

</br>

---
