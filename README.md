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
After installing, please delete the build directory and rebuild following the instrustions from 3.
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
git clone https://github.com/code-iai/iai_kinect2.git
cd iai_kinect2
rosdep install -r --from-paths 
```
(Note: you can get an error like "ERROR: the following packages/stacks could not have their rosdep keys resolved to system dependencies:..."), just ignore it.









