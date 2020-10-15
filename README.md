# robot_localization
This is the base repo for the Olin Computational Robotics Robot Localization project

Features:
+ Resample noise is based on particle variance
+ Custom particle messages
+ Dynamic color visualization
+ maximum certainty
+ modified helper_functions to include lookup_transform and convert_xy_and_theta_to_pose

Potential improvements:
+ Use mode instead of mean 


```
roscore
rosparam set use_sim_time true
roslaunch robot_localizer test_bagfile.launch map_name:=ac109_1
```
