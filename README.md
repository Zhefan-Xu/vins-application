# VINS-application
+ VINS-Mono and Fusion application of different sets of cameras and imu on different board including desktop and jetson xavier
+ Branch : zed-m, pointgrey_myahrs, intel d435i
<br>
<br>

# Index
### 1. [Algorithm & Gpu, Cpu version](#1-algorithm--gpu-cpu-version-1)
### 2. [Parameters](#2-parameters-1)
### 3. Prerequisites
#### ● [OpenCV with CUDA](#-opencv-with-cuda-1)
#### ● [USB performance](#-usb-performance-1)
#### ● [IMU-Camera Calibration](#-calibration--kalibr---synchronization-time-offset-1) : Synchronization, time offset, extrinsic parameter
#### ● [Installation](#-installation-1)
### 4. [Comparison & Application](#4-comparison--application-1)

<br><br><br>

# 1. Algorithm & GPU, CPU version
+ [CPU version](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion)
+ [GPU version](https://github.com/pjrambo/VINS-Fusion-gpu)
<br>

# 2. Parameters
+ Camera frame rate
+ Max tracking Feature number

<br>

# 3. Prerequisites
### ● OpenCV with CUDA
+ Install CUDA : [here](https://askubuntu.com/questions/799184/how-can-i-install-cuda-on-ubuntu-16-04)
+ Build OpenCV with CUDA 
~~~shell
$ sudo apt-get purge libopencv* python-opencv
$ sudo apt-get install -y \
    cmake \
    libavcodec-dev \
    libavformat-dev \
    libavutil-dev \
    libeigen3-dev \ # recommend to build from source : http://eigen.tuxfamily.org/index.php?title=Main_Page
    libglew-dev \
    libgtk2.0-dev \
    libgtk-3-dev \
    libjpeg-dev \
    libpng-dev \
    libpostproc-dev \
    libswscale-dev \
    libtbb-dev \
    libtiff5-dev \
    libv4l-dev \
    libxvidcore-dev \
    libx264-dev \
    qt5-default \
    zlib1g-dev \
    libgl1 \
    libglvnd-dev \
    pkg-config
$ cd <opencv_source_directory>/build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D WITH_CUDA=ON \
      -D CUDA_ARCH_BIN=7.2 \ # check your BIN version : http://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/
      -D CUDA_ARCH_PTX="" \
      -D ENABLE_FAST_MATH=ON \
      -D CUDA_FAST_MATH=ON \
      -D WITH_CUBLAS=ON \
      -D WITH_LIBV4L=ON \
      -D WITH_GSTREAMER=ON \
      -D WITH_GSTREAMER_0_10=OFF \
      -D WITH_QT=ON \
      -D WITH_OPENGL=ON \
      -D CUDA_NVCC_FLAGS="--expt-relaxed-constexpr" \
      -D WITH_TBB=ON \
      ../
~~~
<br>

### ● USB performance
  + Link : [here](https://github.com/KumarRobotics/flea3#optimizing-usb-performance-under-linux)
  + For Xavier : [here](https://devtalk.nvidia.com/default/topic/1049581/jetson-agx-xavier/change-usbcore-usbfs_memory_mb/)
  ~~~shell
  $ sudo ./flash.sh -k kernel -C "usbcore.usbfs_memory_mb=1000" -k kernel-dtb jetson-xavier mmcblk0p1
  ~~~
<br>

### ● Calibration : Kalibr -> synchronization, time offset, extrinsic parameter
+ [Kalibr](https://github.com/ethz-asl/kalibr) -> synchronization, time offset <br>
+ For ZED cameras : [here](https://support.stereolabs.com/hc/en-us/articles/360012749113-How-can-I-use-Kalibr-with-the-ZED-Mini-camera-in-ROS-)

<br>

### ● Installation
<br>

# 4. Comparison & Application
+ /tf vs VINS-Mono on flightgoggles : [youtube](https://youtu.be/U4TJ7ZyfWD8)
+ Loop Fusion vs vins node on flightgoggles : [youtube](https://youtu.be/cvhI_1XQQt4)
+ Real World VINS-Mono with pointgrey cam, myAHRS+ imu on Jetson Xavier : [youtube](https://youtu.be/4qJYoND9OYk)
+ Real World VINS(GPU+version) with pointgrey, myAHRS at Intel i7-8700k, TITAN RTX : [youtube](https://youtu.be/UEZMZMFFhYs)
<br>
