+++
title = 'ORB SLAM3稠密建图'
date = '2022-10-16T15:16:01+08:00'
tags = ['ORB-SLAM3','WSL2','Ubuntu']
categories = ['教程']
image= 'ORB-SLAM3-cover.webp'
+++


## 依赖
### Eigen
[eigen.tuxfamily.org](https://eigen.tuxfamily.org/)
```bash
wget https://gitlab.com/libeigen/eigen/-/archive/3.3.4/eigen-3.3.4.zip
unzip eigen-3.3.4.zip && cd eigen-3.3.4
mkdir build && cd build
cmake ..
sudo make install
sudo cp -r /usr/local/include/eigen3/Eigen /usr/local/include
```
### Pangolin
[Pangolin-Github](https://github.com/stevenlovegrove/Pangolin)
```bash
git clone https://github.com/stevenlovegrove/Pangolin
cd Pangolin/scripts/
rm -rf vcpkg/
git clone https://github.com/microsoft/vcpkg
cd ..
./scripts/install_prerequisites.sh --dry-run recommended
mkdir build && cd build
cmake ..
cmake --build .
sudo make install
```

错误1：Could NOT find OpenGL
```bash
sudo apt install libgl1-mesa-dev
```
错误2：Could not find GLEW
```bash
sudo apt install libglew-dev
```

### OpenCV
[opencv.org](https://opencv.org/)
1. 安装依赖
    ```bash
    sudo apt install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev
    sudo apt install libgtk2.0-dev
    sudo apt install pkg-config
    ```
2. 安装OpenCV
    ```bash
    sudo apt update && sudo apt install g++ unzip wget cmake
    wget -O opencv.zip https://github.com/opencv/opencv/archive/refs/tags/4.4.0.zip
    unzip opencv.zip
    cd opencv-4.4.0/
    mkdir build && cd build
    cmake ..
    cmake --build .
    sudo make install
    ```

### Boost
```bash
sudo apt install libboost-all-dev
```

## 安装PCL
1. 依赖
将以下内容保存为install_pcl_dependences.sh ，使用在ubuntu 命令行终端输入sudo sh install_pcl_dependences.sh 即可进行安装，在下载安装依赖库过程中会提示是否安装，都输入y。（好像没什么用）
```bash
 sudo apt-get update
 sudo apt-get install git build-essential linux-libc-dev
 sudo apt-get install cmake cmake-gui
 sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev
 sudo apt-get install mpi-default-dev openmpi-bin openmpi-common  
 sudo apt-get install libflann1.8 libflann-dev
 sudo apt-get install libeigen3-dev
 sudo apt-get install libboost-all-dev
 sudo apt-get install libvtk5.10-qt4 libvtk5.10 libvtk5-dev
 sudo apt-get install libqhull* libgtest-dev
 sudo apt-get install freeglut3-dev pkg-config
 sudo apt-get install libxmu-dev libxi-dev
 sudo apt-get install mono-complete
 sudo apt-get install qt-sdk openjdk-8-jdk openjdk-8-jre
```

2. 下载源码
```bash
## 下载
wget -O pcl.tar.gz https://github.com/PointCloudLibrary/pcl/archive/refs/tags/pcl-1.12.0.tar.gz
## 解压
tar -zxvf pcl.tar.gz
```

3. 安装
```bash
cd pcl-pcl-1.12.0
mkdir release
cd release
cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX=/usr \ -DBUILD_GPU=ON-DBUILD_apps=ON -DBUILD_examples=ON \ -DCMAKE_INSTALL_PREFIX=/usr .. 
make
sudo make install
```
这个是用apt安装，但是好像版本不对
```bash
sudo apt install libpcl-dev
```

## 安装SLAM
```bash
git clone -b dense_map https://github.com/electech6/ORB_SLAM3_detailed_comments
cd ORB_SLAM3_detailed_comments
chmod +x build.sh
./build.sh  ## 如果报错可以试试打开这个文件把里面的指令一句一句手动执行，`make -j`换成`make`
```

**报错1：**
```bash
fatal error: openssl/md5.h: c
 #include <openssl/md5.h>
          ^~~~~~~~~~~~~~~
```
```bash
sudo apt install libssl-dev
```

未完待续......