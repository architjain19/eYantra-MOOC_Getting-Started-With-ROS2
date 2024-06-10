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
    <h1>Welcome to Task 2</h1>
</center>

---

</br>

> *The aim of Task 2 is to get you ready with small chunk of codes in simulation for further full theme implementation.*

### Update your repository before you move ahead with TASK 2
(***NOTE:** Navigate inside the `src` folder of your workspace, before proceeding further*)

```sh
git stash
```

- Then pull the updated Task 2 commits from the repo using-

```sh
git pull
```

- And again pop your changes you've made before from stash using-

```sh
git stash pop
```

For directly starting with Task 2 - (Make sure you are inside the `src` folder before executing these commands)

```sh
pip3 install cryptocode
sudo cp libgazebo_link_ur5_attacher.so /usr/lib/x86_64-linux-gnu/gazebo-11/plugins/
sudo cp libgazebo_link_attacher.so /usr/lib/x86_64-linux-gnu/gazebo-11/plugins/
```

*(If it doesn't work in the task (i.e. if the plugins are not loaded), replace the plugin path with the output you are getting with $GAZEBO_PLUGIN_PATH)*

> - Do `colcon build` to build the workspace with updated packages.
>
> - **NOTE:** After any changes in any files, to reflect the same on workspace you need to do `colcon build`
>
> - If you want to skip this step of building every time a file (python script) is changed (note: this doesn't include addition of file or addition of folder), you may use the `colcon build --symlink-install` parameter with the build command. (Surf over the internet to find more about it)


---


### This task is divided into *two* parts:

### 2A [**Manipulation with vision**](tasks/task2a/task2a.md)
*Locating Aruco in the world with respect to arm and picking the boxes*


### 2B [**Dock and Place**](tasks/task2b/task2b.md)
*Move the rack around using ebot*

<p></p>

</br>

---
