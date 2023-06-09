# Install guideline for *Nvidia Video Processing Framework*
> This is a guideline for installing https://github.com/NVIDIA/VideoProcessingFramework \
> **Thank you for your efforts : [[Junmin Lee]](https://github.com/jumin-lee)**

## 0. Prerequisites
- Cuda Toolkit
- FFmpeg (with libavfilter >= 7.110.100)
  - check with `ffmpeg -version`
- Cmake >= 3.21
- Ninja Build
- C++ compiler(gcc or g++)
  - Check with `gcc --version` or `g++ --version`

## 1. Cmake Install
### 1-0. Check Cmake version
```bash
cmake --version
```
If the version does not satisfied prerequisites, install the new version in the following manner.

### 1-1. Appropriate version download
Download the tar.gz file from the following link : [[URL]](https://cmake.org/download/)

or use `wget` command as below.
```bash
wget https://github.com/Kitware/CMake/releases/download/v(VERSION_NAME)/cmake-(VERSION_NAME).tar.gz
```
Insert the version you want to install into (VERSION_NAME). Note, our example use 3.26.2.

### 1-2. Install Cmake
- Unzip
```bash
tar -xvf cmake-3.26.2.tar.gz
```

- Install
```bash
cd cmake-3.26.2
./bootstrap
make
sudo make install
```
> If an error for OpenSSL occurs, see [issue A](#OpenSSL).

### 1-3. Check Installed Version
Log out of the terminal and re-enter it, then press `cmake --version` to verify correctly installing Cmake.

## FFmpeg Install
### 2-0. Add Path for Installation
Since FFmpeg library will be installed in `/usr/local/lib`, it is necessary to inform the location.\
Add following command to `~/.bashrc` file.
```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib:/usr/local/lib64
```

or `export LD_LIBRARY_PATH` is already exist, add `:/usr/local/lib:/usr/local/lib64` after Cuda LD_LIBRARY_PATH setting.
```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.7/lib64:/usr/local/lib:/usr/local/lib64
```

After adding the location, press the following command and re-enter the terminal.
```bash
source ~/.bashrc
```

Verify `/usr/local/lib` and `/usr/local/lib64` with `echo $LD_LIBRARY_PATH`.

### ~~2-1. FFmpeg Install(apt-get Install - Not Recommended)~~
> Warning: May not be suitable for Ubuntu ≥ 22.04.
```bash
sudo apt-get install ffmpeg -y
```
Easiest way to install ffmpeg package, but may not contain latest version of ffmpeg.\
If installed, check for version with `ffmpeg -version`

  
### 2-2. FFmpeg Install(git repository install)
- Git Repository Clone
```bash
git clone https://github.com/FFmpeg/FFmpeg.git
```

- Change the version of git to install
```bash
cd FFmpeg
git checkout n5.1.2
git pull
```

- Configure
> If 'nasm/yasm' error occurs, see [issue B](#nasm)
```bash
./configure --enable-shared
```
by applying `--enable-shared` option, set to create a shared library (.so file) instead of the static library (.a file) required by the Nvidia Video Process Framework.

Additionally, if you need libx264 and libx265 for encoder, add additonal options as below. (+'png')
```bash
./configure --enable-shared --enable-gpl --enable-libx264 --enable-libx265 --enable-zlib
```
> If an error saying that 'ERROR: x264 not found using pkg-config', see [issue C](#libx265)

If you need additional options, see [[URL]](https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu#FFmpeg).

- Build
```bash
make
sudo make install
```

### 2-3. Installation Check
Check ffmpeg version with 'ffmpeg -version'.

- Check Library
```bash
ls /usr/local/lib
```
Verify installing shared libraries such as 'libavcodec.so' by above command.
If there are no .so files, re-start installation from step **2-0**.

## 3. NVIDA Video Processing Framework Install
### 3-0. Checklist
- nvcc : `nvcc --version` or `nvcc -V`
- Ninja : `which ninja`
  - If not exist, try `sudo apt-get install ninja-build`
- Nivida Driver : `nvidia-smi`

### 3-1 Installation
- Create new environment
```bash
conda create -n <name> python=<version>
conda activate <name>
```

- Git Clone
```bash
git clone https://github.com/NVIDIA/VideoProcessingFramework.git
```
[[Original Code]](https://github.com/NVIDIA/VideoProcessingFramework)

- Installation
```bash
cd VideoProcessingFramework
pip3 install .
```

### 3-2 Check Installation
```bash
python3
import PyNvCodec
```


---
---
## Issue
<a name="OpenSSL"></a>
### A. OpenSSL issue
If you receive an error that there is no OpenSSL when installing the ./bootstrap, install OpenSSL as below.
```bash
sudo apt install libssl-dev
```
<a name="nasm"></a>
### B. nasm/yasm
If you obtain 'nasm/yasm is too old', you can solve this problem as below.
```bash
sudo apt-get install nasm
```
<a name="libx265"></a>
### C. libx264, libx265, zlib
If you obtain 'ERROR: x264 not found using pkg-config' when installing FFmpeg, you can simply install 'libx264-dev' as below.
```bash
sudo apt install -y libx264-dev
```

However, in the case of 'libx265', you can solve problem by these instructions.\
[[Original URL]](https://bitbucket.org/multicoreware/x265_git/wiki/Home)
```bash
git clone https://bitbucket.org/multicoreware/x265_git.git
cd x265_git/build/linux
./make-Makefiles.bash
make
sudo make install
```

In the case of 'zlib', following instructions can help you.
```bash
sudo apt install zlib1g-dev
```

## Additional Prefix for Configuration
```bash
--enable-gnutls --enable-ladspa --enable-lcms2 --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libdav1d --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librabbitmq --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libsrt --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzimg --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-sndio --enable-pocketsphinx --enable-librsvg --enable-libjxl --enable-librist --enable-libvmaf --enable-crystalhd --enable-libmfx --enable-libsvtav1 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libx264 --enable-libplacebo --enable-librav1e --enable-shared
```
