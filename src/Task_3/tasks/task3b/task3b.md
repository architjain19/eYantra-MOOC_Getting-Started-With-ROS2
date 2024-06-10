<center>
    <h1>Task 3B - Simulation Task - Dock, Pick and Place</h1>
</center>

---

## Task Objective:

In this task you need to pick and place a package box which is on a rack kept away from the arm. Therefore the eBot should navigate towards the rack having the box, dock that rack and bring it in front of the arm to do the manipulation task.

> Install the following packages:
```sh
sudo apt install ros-humble-image-transport ros-humble-image-transport-plugins

```

Make sure your github repo is updated for the task 3B.

- **Step 1:** Save your work, navigate within the `src` folder and run the following command:
```sh
git stash

```

- **Step 2:** Pull the latest repo by:
```sh
git pull
git checkout tags/v2.3.1 . # if doesn't work try `git fetch` and try again

```

- **Step 3:** Pop your work back to the repo:
```sh
git stash pop

```