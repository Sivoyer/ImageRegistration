# ImageRegistration

[![Build Status](https://travis-ci.org/Genometric/ImageRegistration.svg?branch=master)](https://travis-ci.org/Genometric/ImageRegistration)


## Install dependencies
This repository depends on [OpenCV](https://opencv.org) and [OpenSlide](http://openslide.org).

### Install [OpenCV](https://opencv.org):
1. Make sure [Java Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) is installed, and the `PATH` variable is set appropriately. 

       export JAVA_HOME="$(/usr/libexec/java_home -v 1.8)":$PATH

2. Create a virtual environment (e.g., [virtualenv](https://virtualenv.pypa.io/en/stable/)) and activate it.
3. Install `numpy`:

       pip install numpy
       
4. Install dependencies: 

        brew install cmake pkg-config
        brew install jpeg libpng libtiff openexr
        brew install eigen tbb
        
	<sub>Note, if you see an error like `XYZ not linked` (where `XYZ` is a package name), try `brew link XYZ`; and if that gives an error like `Linking /usr/local/Cellar/tbb/2018_U2... Error: Permission denied @ dir_s_mkdir - /usr/local/lib/python2.7/site-packages/TBB-0.1-py2.7.egg-info` then run `chmod 755 /usr/local/lib/pkgconfig` then run `brew link XYZ` again. </sub>

5. Run `brew doctor` to make sure all requirements are installed successfully. 
6. Create and `cd` to a folder where you want to download and build `OpenCV` in. 

        mkdir ~/opencv
        cd ~/opencv

7. Download `opencv-3.X.X` Sources (from [this link](https://opencv.org/releases.html)) and unzip it to the above-created folder.
8. Download `opencv` extras (from [this link](https://github.com/opencv/opencv_contrib/releases)) and unzip it to the above-created folder.
9. `cd` to the unzipped `opencv-3.X.X` folder, and make a build folder.

Your folder structure should now look like this:

```shell
.
└── opencv
    ├── opencv-3.4.1
    │   ├── 3rdparty
    │   ├── CMakeLists.txt
    │   ├── CONTRIBUTING.md
    │   ├── LICENSE
    │   ├── README.md
    │   ├── apps
    │   ├── build
    │   ├── cmake
    │   ├── data
    │   ├── doc
    │   ├── include
    │   ├── modules
    │   ├── platforms
    │   └── samples
    └── opencv_contrib-3.4.1
        ├── CONTRIBUTING.md
        ├── LICENSE
        ├── README.md
        ├── doc
        ├── modules
        └── samples

```

10. cd into your opencv-3.X.X/build folder and run the following `make` command:

```shell
cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D OPENCV_EXTRA_MODULES_PATH=PATH_TO_THE_OPENCV_EXTRAS/opencv_contrib-3.4.1/modules \
      -D PYTHON2_LIBRARY=/usr/lib/libpython2.7.dylib \
      -D PYTHON2_EXECUTABLE=$VIRTUAL_ENV/bin/python \
      -D BUILD_opencv_python2=ON \
      -D BUILD_opencv_python3=OFF \
      -D INSTALL_PYTHON_EXAMPLES=OFF \
      -D INSTALL_C_EXAMPLES=OFF \
      -D BUILD_EXAMPLES=OFF ..
```

11. Run the following commands

```shell
make -j4   # 4 is the number of threads, set it to a value appropriate to your machine. 
sudo make install
cd PATH_TO_YOUR_VIRTUAL_ENV/lib/python2.7/site-packages/
ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so
```


### Install [OpenSlide](http://openslide.org)

```shell
brew install openslide
```
