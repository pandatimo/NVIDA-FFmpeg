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
### 1-0. Check cmake version
```
cmake --version
```
If the version does not satisfied prerequisites, install the new version in the following manner.

### 1-1. Appropriate version download
Download the tar.gz file from the following link.\
URL : [Cmake download](https://cmake.org/download/)

or use ```wget``` commend as follows.\
```
wget https://github.com/Kitware/CMake/releases/download/v(VERSION_NAME)/cmake-(VERSION_NAME).tar.gz
```
Insert the version you want to install into (VERSION_NAME). Note, our example use 3.26.2.

### 1-2. Install
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
