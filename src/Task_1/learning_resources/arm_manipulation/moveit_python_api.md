# Accessing Moveit using Python

In ROS 1, we have `moveit_commander`, since for ROS 2 the commander is under devlopment for `Python`, we will be using the `pymoveit` package from [github link (Credits: AndrejOrsula)](https://github.com/AndrejOrsula/pymoveit2). The customised package for this task has been already added in this repository, so that you need to do much changes to start with.

However we highly encourage you to look into the `pymoveit2/moveit2.py`, to understand the inner working of each of the function and to **alter planning parameters**.

You can go through the examples inside the `pymoveit2/example` folder to access the same and understand how it works.
```sh
# Move to joint configuration
ros2 run pymoveit2 ex_joint_goal.py --ros-args -p joint_positions:="[1.57, -1.57, 0.0, -1.57, 0.0, 1.57]"
# Move to Cartesian pose (motion in either joint or Cartesian space)
ros2 run pymoveit2 ex_pose_goal.py --ros-args -p position:="[0.25, 0.0, 1.0]" -p quat_xyzw:="[0.0, 0.0, 0.0, 1.0]" -p cartesian:=False
# Example of adding a collision object to the planning scene of MoveIt 2
ros2 run pymoveit2 ex_collision_object.py --ros-args -p action:="add" -p position:="[0.5, 0.0, 0.5]" -p quat_xyzw:="[0.0, 0.0, -0.707, 0.707]"

```

- For servoing we have done some changes with `ex_servo.py` file, where the function `servo_circular_motion` is empty, for you to explore by writing your own code (for example making the servo move in circle).
- This changes from original code will help you to execute servoing seemlessly.

---

## Feedback of joint_states or position
- You can get the current joint state of each joint by using `joint_states` topic in ros2.
- If you want to know about the position of the end-effector, you can do `lookup transform` for end-effector w.r.t `base_link`.

---

## Practice Assignment
- Move the end effector by giving velocities to x,y,z variables. So that it can reach a point destination.
- The point can be `[0.35, 0.1, 0.68]` in order of x,y,z with respect to `base_link` frame.
- You have to stop after reaching the destination.

***SIMPLE HINT:** The linear velocity is the unit vector calculated in the direction of current pose to destination pose*.
