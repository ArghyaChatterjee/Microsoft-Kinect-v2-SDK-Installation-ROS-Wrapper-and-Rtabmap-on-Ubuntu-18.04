# ROS-Wrapper-for-Kinect-v2-on-Ubuntu-18.04
1. Download libfreenect2:<br>
```git clone https://github.com/OpenKinect/libfreenect2.git```
2. Before installing a good idea to install opencv then rely as follows:
- one way: <br>
``` sudo apt-get install build-essential cmake pkg-config libturbojpeg libjpeg-turbo8-dev mesa-common-dev freeglut3-dev libxrandr-dev libxi-dev```
- another way:
```
sudo apt-get install libglfw3-dev
sudo apt-get install libopenni2-dev
sudo apt-get install libusb-1.0-0-dev
```
(Note: if "sudo apt-get install libusb-1.0-0-dev" doesn't work or give error, you may need a ladder.) Try:
```
sudo apt-add-repository ppa:floe/libusb
sudo apt-get update
sudo apt-get install libusb-1.0-0-dev
```
3. Start Installation (It will be installed by default in /usr/local):
```
cd libfreenect2
mkdir build 
cd build
cmake ..
make
sudo make install
```
(Note: you can get an error like "CMake Error at /usr/share/cmake-3.9/Modules/FindPackageHandleStandardArgs. cmake:137 (message):Could NOT find TurboJPEG (missing: TurboJPEG_INCLUDE_DIRS TURBOJPEG_WORKS)...), Then try: <br>
```sudo apt-get install libturbojpeg0-dev``` <br>
After installing, please delete the build directory and rebuild following the instrustions from 3. <br>
4. Set the udev rules for communicating with device: <br>
```sudo cp libfreenect2/platform/linux/udev/90-kinect2.rules /etc/udev/rules.d/``` <br>
5. Replug the Microsoft Kinect Xbox One. Then run in the build directory:
- ```./bin/Protonect``` <br>
(Note: If you are more advanterous), please run:
- ```./bin/Protonect gl``` to test OpenGL support.
- ```./bin/Protonect cl``` to test OpenCL support.
- ```./bin/Protonect cpu``` to test CPU support.
6. Now for ROS wrapper installation for kinect v2, execute:
```
cd ~/catkin_ws/src/
git clone https://github.com/ArghyaChatterjee/ROS-Wrapper-for-Kinect-v2-on-Ubuntu-18.04.git
cd iai_kinect2
rosdep install -r --from-paths 
```
(Note: you can get an error like "ERROR: the following packages/stacks could not have their rosdep keys resolved to system dependencies:..."), just ignore it and continue. <br>
```
cd ~/catkin_ws
catkin_make -DCMAKE_BUILD_TYPE="Release"
```
7. After successful installation, source the environment: <br>
```source ~/catkin_ws/devel/setup.bash``` <br> 
8. On the same terminal, execute: <br>
```roslaunch kinect2_bridge kinect2_bridge.launch``` <br>
On another terminal, execute: <br>
```
source ~/catkin_ws/devel/setup.bash
rosrun kinect2_viewer kinect2_viewer
``` 
9. If you want to see the rtabmap, open a new terminal and make sure no other program is running. Execute:
```
sudo apt-get install ros-melodic-rtabmap-ros
cd ~/catkin_ws
source ~/catkin_ws/devel/setup.bash
roslaunch kinect2_bridge kinect2_bridge.launch
```
In another terminal, execute: <br>
```
roslaunch rtabmap_ros rgbd_mapping_kinect2.launch resolution:=hd
``` 
<br>
10. If you want to see the rtabmap with rviz:
- One way:
For openning with default rviz, move to /opt/ros/melodic/share/rtabmap_ros/launch directory and open rgbd_mapping_kinect2.launch file. Change rviz (line number 25) to "true" and save the file. Now open a new terminal and make sure no other program is running. Execute:
```
cd ~/catkin_ws
source ~/catkin_ws/devel/setup.bash
roslaunch kinect2_bridge kinect2_bridge_default_rviz.launch
``` 
- Second way: 
If you want to see the rtabmap with custom rviz (prepared by me), open a new terminal and make sure no other program is running. Execute:
```
cd ~/catkin_ws
source ~/catkin_ws/devel/setup.bash
roslaunch kinect2_bridge kinect2_bridge_custom_rviz_qhd.launch  #to open qhd video stream in ROS.
roslaunch kinect2_bridge kinect2_bridge_custom_rviz_hd.launch   #to open hd video stream in ROS.
roslaunch kinect2_bridge kinect2_bridge_custom_rviz_sd.launch   #to open sd video stream in ROS.
```
# Special thanks to:
1. https://github.com/OpenKinect/libfreenect2
2. https://github.com/code-iai/iai_kinect2
3. https://github.com/Kinect/PyKinect2
4. https://github.com/occipital/OpenNI2





