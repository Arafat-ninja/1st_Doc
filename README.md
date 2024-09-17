# 1st_Doc

## Project Overview

This project contains documentation created using Sphinx and hosted on Read the Docs. The documentation outlines the installation process for several essential libraries, including `glog`, `eigen`, `ceres-solver`, `yaml-cpp`, and `OpenCV`.

The shell script provided in this repository automates the cloning, building, and installation of these libraries on a Linux-based system.

## Prerequisites

Before running the script, ensure the following:
- You have a Linux-based system (such as Ubuntu).
- You have `sudo` access to install necessary packages.
- You have configured proxy settings (if required) using `proxychains4`.

## Installation

1. Clone this repository to your local machine:
   ```bash
   git clone git@github.com:Arafat-ninja/1st_Doc.git
   cd 1st_Doc
   ```

2. Run the shell script to install all required libraries:
   ```bash
   chmod +x install_libraries.sh
   ./install_libraries.sh
   ```

   This script will create an `env` directory in your home folder and install the following libraries:
   - `glog`
   - `eigen`
   - `ceres-solver`
   - `yaml-cpp`
   - `OpenCV`

3. Verify that all libraries were installed successfully by checking their version or include paths in `/usr/local/include`.

## Libraries Installed

The script installs the following libraries:

- **glog**: A C++ logging library from Google.
- **eigen**: A C++ template library for linear algebra.
- **ceres-solver**: A C++ library for modeling and solving large, complicated optimization problems.
- **yaml-cpp**: A YAML parser and emitter for C++.
- **OpenCV**: A library for computer vision and image processing.

## How to Contribute

Feel free to fork this repository, create new branches, and submit pull requests with improvements or additional documentation.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

If you have any questions or issues with the project, feel free to contact me via [GitHub Issues](https://github.com/Arafat-ninja/1st_Doc/issues).
```

你可以直接在 GitHub 页面上的 README 编辑框中粘贴此内容并保存。

如果有任何问题或需要进一步修改，随时告诉我！
