# d435i_depth
URDF package for intel realsense d435i depth camera with gazebo plugin installation instructions
![image](https://github.com/user-attachments/assets/86911cac-7df3-476e-be01-a371d55ac442)

Clone this repository into your robot workspace:
```console
git clone https://github.com/nathanshankar/d435i_depth.git
```
Install realsense libraries in your system:
```console
sudo apt-get install ros-$ROS_DISTRO-realsense2-camera
```
Once in your home directory execute the following commands:
```console
mkdir -p ros2_ws/src
cd ~/ros2_ws/src
git clone https://github.com/IntelRealSense/realsense-ros.git -b ros2-development
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

