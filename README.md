# robot_localization
The code in this repository implements a ParticleFilter, which is tested on board a Neato (robotic vacuum equipped with a LiDAR) using ROS bagfiles that are collected from a physical platform. This was created as part of the Olin Computational Robotics class in Fall 2020 as part of the Robot Localization project

Contributors:
[Amy Phung](https://github.com/AmyPhung),
[Eamon O'Brien](https://github.com/EamonCOBrien),
[Emma Pan](https://github.com/epan547)
## At-a-glance
#### Features:
+ Resample noise is based on particle variance
+ Custom particle messages
+ Dynamic color visualization
+ maximum certainty
+ modified helper_functions to include lookup_transform and convert_xy_and_theta_to_pose



## Details
#### Project goal
The objective of implementing a ParticleFilter is to create a method of figuring out where the robot is within a known map. Although there are mathematically straightforward ways to compute this, there are usually runtime considerations that prevent these from being implemented as-is. In a particle filter, we attempt to compute a "good enough" approximation by tracking and updating a series of poses, which we assign weights to that represent our level of confidence in that particular pose.

#### What we did
The following steps are implemented in our ParticleFilter
<!-- TODO: make this into a draw.io diagram & upload to repo -->
+ Create a series of particles with varying positions and poses around our initial estimate (high uncertainty, lots of variation)
+ Compute weights for each particle
    + Line up the center of the lidar data with the particle
    + For each point in the lidar, compute what map position that'd be
    ```
    dxs = msg.ranges * np.cos(np.degrees(angles + p.theta))
    dys = msg.ranges * np.sin(np.degrees(angles + p.theta))
    ```
    + For each of the projected lidar points, compute the distance to the nearest point in the map
       + If the projection is off the map, discard the projection
    + Compute the average distance
    + Create a weight value that is inversely proportional to the square of the distance
+ Normalize weights (adjust weights such that their sum equal 1)
+ Update most likely robot pose (currently done with an average of the particles)
+ Resample particles (randomly choose particles from a weighted set, add noise that is proportional to the variance)
+ Go back to compute weights

#### Key Design Decisions
<!-- TODO: Expand this -->
+ custom rviz display for weights
+ creating a particlearray message

#### Notable Challenges
+ parameter tuning
+

#### Potential improvements:
+ Use mode instead of mean
+ Set a cap on confidence level (failure mode: it becomes overly confident, particularly while turning, and the variance and noise drop to 0)
+ dynamic reconfigure window

#### Lessons Learned:


<!-- How did you solve the problem? (Note: this doesn’t have to be super-detailed, you should try to explain what you did at a high-level so that others in the class could reasonably understand what you did). -->
<!-- Describe a design decision you had to make when working on your project and what you ultimately did (and why)? These design decisions could be particular choices for how you implemented some part of an algorithm or perhaps a decision regarding which of two external packages to use in your project.
What if any challenges did you face along the way?
What would you do to improve your project if you had more time?
Did you learn any interesting lessons for future robotic programming projects? These could relate to working on robotics projects in teams, working on more open-ended (and longer term) problems, or any other relevant topic. -->


```
roscore
rosparam set use_sim_time true
roslaunch robot_localizer test_bagfile.launch map_name:=ac109_1
```
