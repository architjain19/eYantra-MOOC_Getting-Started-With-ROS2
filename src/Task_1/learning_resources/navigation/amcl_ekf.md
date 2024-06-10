# Adaptive Monte Carlo Localization (AMCL) and Extended Kalman filter (EKF)

> Note: The goal of this section is to just give you the intuition of how AMCL works and not to go in to depth in mathematics.

AMCL is a probabilistic localization system for a robot moving in 2D. Given a map of the environment, the algorithm estimates the position and orientation of a robot as it moves and senses the environment



**Monte Carlo Localization algorithm (MCL)**

The algorithm uses a known map of the environment, range sensor data, and odometry sensor data. To localize the robot, the MCL algorithm uses a particle filter to estimate its position. The particles represent the distribution of the likely states for the robot. Each particle represents the state of the robot.

* **Initialization**: The robot starts with random particle estimates of its location and heading based on a map. Each particle represents a potential state.

* **Sensor-Based Refinement**: The filter compares these particles with actual Lidar sensor data, discarding poorly matched ones.

* **Weighted Resampling**: Particles are assigned weights based on their scene match with the actual robot pose, and resampling is performed to concentrate particles around the true pose.

* **Adaptive Particle Management**: As the robot moves, particles are updated, and the algorithm adjusts the number of particles using Kullback-Leibler divergence. This process, known as **Adaptive Monte Carlo Localization**, optimizes accuracy and computational efficiency.

**Extended Kalman filter (EKF)**

* **Estimation Tool**: EKF is a mathematical tool used in robotics and navigation to figure out where a robot or object is and how it's moving.

* **Handling Complexity**: It's good at dealing with systems that are a bit complicated but not too crazy. It simplifies these systems to make them easier to work with.

* **State and Uncertainty**: EKF gives you an estimate of the current state (like the robot's position and speed) along with how sure or unsure you should be about that estimate.

> To simply to this here, **AMCL** is a `global localization algorithm` in the sense that it fuses LIDAR scan matching with a source of odometry to provide an estimate of the robot's pose w.r.t a global map reference frame. It is common to use an **EKF** such as those implemented in the `robot_localization` package to fuse wheel odometry with an IMU (or other sensors) and create an improved odometry estimate (`local pose estimation`) for AMCL


Reference:

1.  [https://www.youtube.com/watch?v=htE5cClSy4Y&t=228s](https://www.youtube.com/watch?v=htE5cClSy4Y&t=228s)
2. [http://www.cs.cmu.edu/~rasc/Download/AMRobots5.pdf](http://www.cs.cmu.edu/~rasc/Download/AMRobots5.pdf)
3. Probabilistic Robotics, Book by Dieter Fox, Sebastian Thrun, and Wolfram Burgard
4.  [https://www.youtube.com/watch?v=NrzmH_yerBU](https://www.youtube.com/watch?v=NrzmH_yerBU)



