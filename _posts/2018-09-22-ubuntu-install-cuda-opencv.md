---
title: "ubuntu中源码编译安装cuda版opencv"
category: other
layout: post
tags: [other]
date: '2018-09-22 18:00:24'
---

### 安装

```
#下载opencv源码
git clone https://github.com/opencv/opencv.git
cd opencv
git checkout remotes/origin/3.4
#下载extras源码
git clone https://github.com/opencv/opencv_extra.git
cd opencv_extra
git checkout remotes/origin/3.4
#编译安装
cd opencv
cmake .. -DPYTHON_DEFAULT_EXECUTABLE=/data/ruben/anaconda3/bin/python -DBUILD_opencv_python2=Off -DBUILD_opencv_python3=On -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -DCMAKE_BUILD_TYPE=RELEASE -DWITH_CUDA=ON -DENABLE_FAST_MATH=1 -DCUDA_FAST_MATH=1 -DWITH_CUBLAS=1 -DCUDA_GENERATION=Auto -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda
make -j12
sudo make install
```

### 可能遇到的问题


- 1.卸载opencv
在安装之前需要卸载之前安装的opencv，执行下面的命令：
```
sudo updatedb
locate OpenCVConfig.cmake
```
根据输出找出已经安装的opencv路径，然后卸载即可。
   
   
- 2.nvcc fatal: Unsupported gpu architecture 'compute_60'
这个问题的原因是需要更新cuda，打开链接[link](https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_10.0.130-1_amd64.deb)，保存到本地路径。

依次执行：
 ```
sudo dpkg -i cuda-repo-ubuntu1604_10.0.130-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub`
sudo apt-get update
sudo apt-get install cuda
sudo apt-get install cuda-toolkit-8-0 
```
即可。

- 3.fatal error: ImfChromaticities.h: No such file or directory

```
sudo apt-get install libopenexr-dev
```


- 4.完整的cmake参考

```
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DBUILD_PNG=OFF \
    -DBUILD_TIFF=OFF \
    -DBUILD_TBB=OFF \
    -DBUILD_JPEG=OFF \
    -DBUILD_JASPER=OFF \
    -DBUILD_ZLIB=OFF \
    -DBUILD_EXAMPLES=ON \
    -DBUILD_opencv_java=OFF \
    -DBUILD_opencv_python2=ON \
    -DBUILD_opencv_python3=OFF \
    -DWITH_OPENCL=OFF \
    -DWITH_OPENMP=OFF \
    -DWITH_FFMPEG=ON \
    -DWITH_GSTREAMER=OFF \
    -DWITH_GSTREAMER_0_10=OFF \
    -DWITH_CUDA=ON \
    -DWITH_GTK=ON \
    -DWITH_VTK=OFF \
    -DWITH_TBB=ON \
    -DWITH_1394=OFF \
    -DWITH_OPENEXR=OFF \
    -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda \
    -DCUDA_ARCH_BIN='3.0 3.5 5.0 6.0 6.2' \
    -DCUDA_ARCH_PTX="" \
    -DINSTALL_C_EXAMPLES=ON \
    -DINSTALL_TESTS=OFF \
    -DOPENCV_TEST_DATA_PATH=../opencv_extra/testdata \
    ../opencv
```
