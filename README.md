xml_based_urdfparser
====================

a python urdf parser based on xml minidom

Install
=======

Run python setup.py install

Features
========

Generate urdf and xacro files for aldebaran robots (using Aldebaran URDFs as input files https://github.com/keulYSMB/nao_robot/tree/devel/nao_description/bin)
Automatic generation of the entire URDF file or of specific parts of the robot as xacro files.

Dependencies 
============

xml.dom
argparse
subprocess
the library provided in this package
nao_meshes package if you want the official Aldebaran meshes

Changes
=======
06/25/2014
----------
- add transmission and gazebo tags to the parser library
- add methods to library : add_material, add_gazebo
- export xacro files using kinematics chains
- fix scale of meshes in the output files
- New input parameter : --meshes

06/26/2014
----------
- More generic mesh path : file:/// became package://
- Simplify exportXacroRobotChain function
- Collisions generated automatically whatever the meshes are
- Modify gazebo class to handle gazebo without reference
- Created JointPlugin class : parsing and export work
- validated: gazebo joints, gazebo links without plugin, gazebo robot simulation

06/27/2014
----------
- Created plugin classes : GenericPlugin, MimicJointPlugin, BumperPlugin, LaserPlugin, IMUPlugin, VideoPlugin, OdometryPlugin, CameraPlugin,
- Created Sensor class but not fully implemented

06/30/2014
----------
- Created : IMU_LaserPlugin, CameraSensor, Range, Scan, Horizontal, Ray, Image, Noise
- Validated all plugins : still have to debug HokuyoSensor

07/01/2014
----------
- Debugged/Validated all sensors + plugins
- Solved the sensor/pose issue (not the same format as urdf)

07/02/2014
----------
- split library into 2 files :
        - urdf.py
        - gazebo.py
- packaging the lib to use it as a python module
- catkinized package

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

