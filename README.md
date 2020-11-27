TurtleBot Arm
=============

ROS Indigo version of turtlebot arm code with support for PhantomX Pincher. It should work on ROS Hydro as well. Package turtlebot_arm_moveit_demos provides examples to start playing with the arm on MoveIt!, while the indigo turtlebot_arm_block_manipulation provides a more complete and interesting demo.

## Selecting Arm Type
By default the code uses the original white/green TurtleBot arm.  To use the PhantomX Pincher, set the environment variable "TURTLEBOT_ARM1" to pincher. You will need arbotix_ros version 0.11.0 or higher for PhantomX Pincher.

## Attaching the Arm to a Robot
Open your xacro-macro-magic URDF, and add something like:

       <include filename="$(find turtlebot_arm_description)/urdf/$(optenv TURTLEBOT_ARM1 turtlebot)_arm.xacro" />
       <turtlebot_arm parent="base_link" color="white" gripper_color="green"
                 joints_vlimit="1.571" pan_llimit="-2.617" pan_ulimit="2.617">
          <origin xyz="0 0 1"/>
        </turtlebot_arm>

This will attach a turtlebot arm to your robot. Replace base_link with the base link you use to attach the arm, and change the origin as needed. Apart from color, you can configure joint velocity limit and lower/upper limits for the first joint (arm_shoulder_pan) to allow access to different operational areas, e.g. left handed vs. right handed robot

## Running MoveIt
Ensure you have all the required dependencies by running:

       cd turtlebot_arm
       rosdep install --from-paths -i -y src

Before you start playing, calibrate your camera extrinsic parameters following [this tutorial](http://wiki.ros.org/turtlebot_kinect_arm_calibration/Tutorials/CalibratingKinectToTurtleBotArm)

The turtlebot_arm_moveit_config/demo.launch is a bit wonky, but the move_group action underlying it works fine. To test your installation, run the pick and place demo from turtlebot_arm_moveit_demos, e.g.:

       rosrun turtlebot_arm_moveit_demos pick_and_place.py
