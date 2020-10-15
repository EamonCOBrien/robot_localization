# robot_localization
This is the base repo for the Olin Computational Robotics Robot Localization project

Features:
+ Resample noise is based on particle variance
+ Custom particle messages
+ Dynamic color visualization
+ maximum certainty

Potential improvements:
+ Lidar to base_link tf


```
roscore
rosparam set use_sim_time true
roslaunch robot_localizer test_bagfile.launch map_name:=ac109_1
```
