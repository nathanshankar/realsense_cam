# ROS2 d455 depth camera with Ignition Gazebo
URDF package for intel realsense d455 depth camera with gazebo plugin installation instructions
![image](https://github.com/user-attachments/assets/86911cac-7df3-476e-be01-a371d55ac442)

Clone this repository into your robot workspace:
```console
git clone https://github.com/nathanshankar/d455_depth.git
```
Install realsense libraries in your system:
```console
sudo apt-get install ros-$ROS_DISTRO-realsense2-*
```
Once in your home directory execute the following commands:
```console
mkdir -p ros2_ws/src
cd ~/ros2_ws/src
git clone https://github.com/IntelRealSense/realsense-ros.git -b ros2-master
git clone https://github.com/pal-robotics/realsense_gazebo_plugin.git -b foxy-devel
git clone https://github.com/koichirokato/gazebo_sensor_ros2
cd ..
colcon build --symlink-install
source install/setup.bash
```

### Set Environment value
Run the following command to load the RealSense model file. (It will work without running it, but the model will not appear on Gazebo.)
```console
export GAZEBO_MODEL_PATH=~/ros2_ws/install/realsense2_description/share/realsense2_description/meshes/:$GAZEBO_MODEL_PATH
```

# Camera visualization
To view the camera in rviz open your robot workspace build and source the workspace and run:
```console
ros2 launch d455_depth depth.launch.py
```

The workspace contains the gazebo plugins and scripts and nothing has to be changed. To attach the camera to your robot add the following lines in your robot description:

To add the d455 depth camera's urdf:
```xacro
<xacro:include filename="$(find d455_depth)/urdf/d455_gz.urdf.xacro"/>
```

Add a joint to your robot using:
```xacro
<joint name="d_cam_joint" type="fixed">
    <origin xyz="0 0 0" rpy="0 0 0"/>
    <parent link="THE_LINK_THE_CAMERA_IS_ATTACHED_TO"/>
    <child link="base_screw"/>
</joint>
```
and make necessary adjustments to align the camera with your robot.
