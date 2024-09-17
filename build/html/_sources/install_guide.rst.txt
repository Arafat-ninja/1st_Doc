Installing Essential Libraries Using a Shell Script
===================================================

This document provides detailed instructions on how to use a shell script to clone, build, and install several essential libraries: `glog`, `eigen`, `ceres`, `yaml-cpp`, and `opencv`. The script is designed to automate the installation process to save time and ensure consistency across environments.

Prerequisites
--------------
Before running the script, ensure that:
- Your system is running a Linux distribution like Ubuntu.
- You have `sudo` access to install necessary system dependencies.
- Proxy settings (e.g., `proxychains4`) are properly configured if required.

Steps to Run the Script
------------------------
1. **Clone or Download the Script**
   You can copy the shell script from the following section or download it from a version control repository if available.
   
2. **Run the Script**
   Make sure the script has execute permissions, then run it as shown below:
   
   .. code-block:: bash
   
      chmod +x install_libraries.sh
      ./install_libraries.sh

   The script will create an `env` directory in your home folder, download, build, and install all the libraries inside it.

Script Explanation
-------------------
Here’s an overview of the key sections of the script:

1. **Creating the Environment Directory**
   The script first creates the `~/env` directory to organize the installation files.
   
   .. code-block:: bash

      mkdir -p ~/env
      cd ~/env

2. **Installing Essential Packages**
   The script installs several essential packages required for compiling and building the libraries:
   
   .. code-block:: bash
   
      sudo apt-get install -y build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

   These include compilers, version control tools, and multimedia libraries necessary for OpenCV.

3. **Library Installation Functions**
   
   The script defines functions for installing each library. Each function follows a similar structure:
   
   - Clone the source code from the official repository.
   - Checkout a specific version (optional but recommended for stability).
   - Create a `build` directory, configure the build with CMake, and compile the source code.

   Below are detailed explanations of each function:

   **glog Installation**
   ---------------------
   The `install_glog` function installs Google’s logging library, `glog`. It ensures that all dependencies are installed first:
   
   .. code-block:: bash
   
      sudo apt-get install -y autoconf automake libtool
      proxychains4 git clone https://github.com/google/glog.git
      cd glog
      git checkout v0.6.0
      mkdir build
      cd build
      proxychains4 cmake .. -DCMAKE_BUILD_TYPE=Release
      make -j$(nproc)
      sudo make install

   **eigen Installation**
   ---------------------
   The `install_eigen` function installs the Eigen linear algebra library, used extensively in computer vision and robotics:
   
   .. code-block:: bash

      proxychains4 git clone https://gitlab.com/libeigen/eigen.git
      cd eigen
      git checkout 3.4.0
      mkdir build
      cd build
      proxychains4 cmake .. -DCMAKE_BUILD_TYPE=Release
      make -j$(nproc)
      sudo make install

   **ceres Installation**
   ---------------------
   The `install_ceres` function installs Ceres Solver, which is a robust nonlinear optimization library, commonly used in SLAM and computer vision tasks:
   
   .. code-block:: bash

      sudo apt-get install -y libgoogle-glog-dev libgflags-dev libatlas-base-dev libsuitesparse-dev
      proxychains4 git clone https://github.com/ceres-solver/ceres-solver.git
      cd ceres-solver
      git checkout 2.0.0
      mkdir build
      cd build
      proxychains4 cmake .. -DBUILD_TESTING=OFF -DBUILD_EXAMPLES=OFF
      make -j$(nproc)
      sudo make install

   **yaml-cpp Installation**
   ------------------------
   The `install_yaml_cpp` function installs `yaml-cpp`, which is a YAML parser and emitter:
   
   .. code-block:: bash

      proxychains4 git clone https://github.com/jbeder/yaml-cpp.git
      cd yaml-cpp
      git checkout yaml-cpp-0.7.0
      mkdir build
      cd build
      proxychains4 cmake .. -DYAML_BUILD_SHARED_LIBS=ON
      make -j$(nproc)
      sudo make install

   **OpenCV Installation**
   -----------------------
   The `install_opencv` function installs OpenCV, a popular library for computer vision and image processing. The script also installs `opencv_contrib`, which contains additional modules for advanced functionalities.
   
   .. code-block:: bash

      proxychains4 git clone https://github.com/opencv/opencv.git
      cd opencv
      git checkout 4.5.3
      cd ..
      proxychains4 git clone https://github.com/opencv/opencv_contrib.git
      cd opencv_contrib
      git checkout 4.5.3
      cd ../opencv
      mkdir build
      cd build
      proxychains4 cmake -D CMAKE_BUILD_TYPE=RELEASE \
            -D CMAKE_INSTALL_PREFIX=/usr/local \
            -D INSTALL_C_EXAMPLES=ON \
            -D INSTALL_PYTHON_EXAMPLES=ON \
            -D WITH_TBB=ON \
            -D WITH_V4L=ON \
            -D OPENCV_PYTHON3_INSTALL_PATH=$(python3 -c "import site; print(site.getsitepackages()[0])") \
            -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
            -D BUILD_EXAMPLES=ON ..
      make -j$(nproc)
      sudo make install

Verifying Installation
----------------------
After the script completes, the installed libraries should be available in your system for use in C++ or Python projects.

Troubleshooting
---------------
If any of the installations fail, check the following:
- Network settings, especially if you are using a proxy (e.g., `proxychains4`).
- Dependencies or missing packages that are not covered by the script.
- Disk space and available resources for compiling large projects like OpenCV.

Conclusion
----------
This shell script simplifies the installation process of essential libraries for computer vision, optimization, and system logging. By automating the steps, it ensures consistency and saves valuable time.
