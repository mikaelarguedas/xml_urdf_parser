xml_based_urdfparser
====================

a python urdf parser based on xml minidom

Features
========

Generate urdf and xacro files for aldebaran robots (using Aldebaran URDFs as input files https://github.com/keulYSMB/nao_robot/tree/devel/nao_description/bin)
Automatic generation of the entire URDF file or of specific parts of the robot as xacro files.

Dependencies 
============

- xml.dom
- argparse
- subprocess
- the library provided in this package
- nao_meshes package if you want the official Aldebaran meshes

Install
=======

- Download nao_meshes:
    -- Download https://github.com/vrabaud/nao_meshes/blob/master/binaries/naomeshes-0.6.2-linux-x64-installer.run
    -- run the installer : this will extract a catkin package named nao_meshes at the chosen location
- Download Nao_Original_URDF:
    -- Download https://github.com/keulYSMB/AldebaranURDF/blob/master/bin/naourdf-0.6-linux-x64-installer.run
    -- run the installer : this will extract the NAOH25V40.urdf file at the chosen location
- clone the xml_urdf_parser catkin package : https://github.com/keulYSMB/xml_urdf_parser
- run catkin_make in your workspace to index nao_meshes and xml_urdf_parser

How to use it
=============
- rosrun xml_urdf_parser modify_urdf -i PATH/TO/OFFICIAL/ALDEBARAN/URDF -o PATH/TO/OUTPUT/URDF/FILE -m Type of mesh ("dae" for gazebo, "mesh" for rviz) -x xacrofiles wanted : ("urdf" for a complete URDF file, "robot" for all the kinematics chains of the robot, "legs" for legs kinematics chains, "arms" for arms kinematics chains...)
- generate the urdf (if -x != "urdf") : rosrun xacro xacro.py PATH/TO/OUTPUT/URDF/FILErobot.xacro > /WANTED/URDF/FILE/LOCATION

Visualize the results:
- RVIZ : roslaunch xml_urdf_parser display_meshes.launch pmodel:=PATH/TO/URDF/FILE
- Gazebo: rosrun gazebo_ros spawn_model -file /home/marguedas/Documents/URDF_XACRO/nao.urdf  -urdf -x 0 -y 1 -z 0.5 -model nao


Changes
=======

07/03/2014
---------
- recatkinized package : update __ini__.py, CMakeLists.txt
- add sonar frames to urdf generation
- bugfix : path of included files in ..robot.xacro file

TODO
======
- add transmission to urdf + ros_controller to perform real simulation 
- get finger Frames and SensorFrames from aldebaran documentation
- fix joints:
    - get L/RHand from documentation : limits
    - mimic joints for pelvis and fingers : add libroboticsgroup_gazebo_mimic_joint_plugin.so
- we can parse gazebo tags, we still need to add the following automatically:
    - mimic joints :libroboticsgroup_gazebo_mimic_joint_plugin.so
    - disable link : libroboticsgroup_gazebo_disable_link_plugin.so
    - ROS control : libgazebo_ros_control.so
 
Missing Resources
=================
- Finger and toes frames from Aldebaran doc
- Transmission elements
- Missing mimic joints (we can add them by hand for know)

