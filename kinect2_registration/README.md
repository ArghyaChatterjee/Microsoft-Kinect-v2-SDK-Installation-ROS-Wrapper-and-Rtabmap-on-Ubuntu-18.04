# Kinect2 Registration

## Description

This is a library for projecting the depth image obtained by Kinect like sensors to a color image. It has a OpenCL implementation for registering the depth image, to reduce CPU load.

## Dependencies

- ROS Melodic
- OpenCV
- Eigen (optional, but recommended)
- OpenCL (optional, but recommended)

At least one of OpenCL or Eigen has to be installed. If OpenCL is not installed the CPU will be used. For optimal performance OpenCL is recommended.

*for the ROS packages look at the package.xml*

