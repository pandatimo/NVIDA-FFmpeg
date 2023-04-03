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

### 1-1. Latest version download
Download the zip file from the following link
