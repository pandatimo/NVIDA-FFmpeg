# Install guideline for *Nvidia Video Processing Framework*
> This is a guideline for installing https://github.com/NVIDIA/VideoProcessingFramework

## 0. Prerequisites
- Cuda Toolkit
- FFmpeg (with libavfilter >= 7.110.100)
  - check with ```ffmpeg -version```
- Cmake >= 3.21
- Ninja Build
- C++ compiler(gcc or g++)
  - Check with ```gcc --version``` or ```g++ --version```

## 1. Cmake Install
### 1-0. Check Cmake version
```
cmake --version
```
If the version does not satisfied prerequisites, install the new version in the following manner.

### 1-1. Appropriate version download
Download the tar.gz file from the following link.\
[URL] : [Cmake download](https://cmake.org/download/)

or use ```wget``` commend as below.
```
wget https://github.com/Kitware/CMake/releases/download/v(VERSION_NAME)/cmake-(VERSION_NAME).tar.gz
```
Insert the version you want to install into (VERSION_NAME). Note, our example use 3.26.2.

### 1-2. Install Cmake
- Unzip
```
tar -xvf cmake-3.26.2.tar.gz
```

- Install
```
cd cmake-3.26.2
./bootstrap
make
sudo make install
```
> If an error for OpenSSL occurs, see [issue A](#OpenSSL).

### 1-3. Check Installed Version
Log out of the terminal and re-enter it, then press ```cmake --version``` to verify correctly installing Cmake.

## FFmpeg Install
### 2-0. Add Path for Installation
Since FFmpeg library are installed in ```/usr/local/lib```, it is necessary to inform the location.\
Add following commend to ```~/.bashrc``` file.
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib:/usr/local/lib64
```

or ```export LD_LIBRARY_PATH``` is already exist, add ```:/usr/local/lib:/usr/local/lib64``` after Cuda LD_LIBRARY_PATH setting.
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.7/lib64:/usr/local/lib:/usr/local/lib64
```





## Issue
<a name="OpenSSL"></a>
### A. OpenSSL issue
If you receive an error that there is no OpenSSL when installing the ./bootstrap, install OpenSSL as below.
```
sudo apt install libssl-dev
```
