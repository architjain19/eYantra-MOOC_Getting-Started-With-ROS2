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

> *The aim of Task 3 is to get you hands on with remote hardware and simultaneously work on your program in simulation to progress towards full theme implementation.*

> Install the following packages:
```sh
sudo apt install ros-humble-image-transport ros-humble-image-transport-plugins

```

### Update your repository before you move ahead with TASK 3
(***NOTE:** Navigate inside the `src` folder of your workspace, before proceeding further*)

```sh
git stash
```

- Then pull the updated Task 3 commits from the repo using-

```sh
git pull
git checkout tags/v2.3.1 . # if doesn't work try `git fetch` and try again
```

- And again pop your changes you've made before from stash using-

```sh
git stash pop
```

> - Do `colcon build` to build the workspace with updated packages.
>
> - **NOTE:** After any changes in any files, to reflect the same on workspace you need to do `colcon build`
>
> - If you want to skip this step of building every time a file (python script) is changed (note: this doesn't include addition of file or addition of folder), you may use the `colcon build --symlink-install` parameter with the build command. (Surf over the internet to find more about it)

---


### This task is divided into *two* parts:

### 3A [**Remote Hardware Task - Object Pose Estimation**](tasks/task3a/task3a.md)
*Locating Aruco in the camera view with respect to arm and sending transforms*

### 3B [**Simulation Task - Dock, Pick and Place**](tasks/task3b/task3b.md)
*Dock the rack using ebot towards robot arm and pick and place in dropbox*

<p></p>

</br>

---
