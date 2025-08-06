# pinocchio installation guide
## Github
https://github.com/stack-of-tasks/pinocchio
## Installation
### 1. dependence
egien
```
sudo apt update
sudo apt install libeigen3-dev
```
### 2. download the source
```
git clone --recursive https://github.com/stack-of-tasks/pinocchio
cd pinocchio
git checkout master
mkdir build && cd build
```
### 3. build
#### 1. change `CMakeLists.txt`
注意：因为我们需要的是`C++`库，所以不需要同时生成`Python`版本的编译文件所以在`Cmake`前，要修改`Pinocchio`中的`CmakeLists.txt`文件来关闭这个选项，将下面的`BUILD_PYTHON_INTERFACE`的`ON`改为`OFF`即可。
如果一开始没有关闭`BUILD_PYTHON_INTERFACE`，会在编译时在里面`python`文件下面报错。

```
OPTION(BUILD_BENCHMARK "Build the benchmarks" OFF)
OPTION(BUILD_UTILS "Build the utils" OFF)
OPTION(BUILD_PYTHON_INTERFACE "Build the Python bindings" ON)
OPTION(BUILD_WITH_COMMIT_VERSION "Build libraries by setting specific commit version" OFF)
```
#### 2. cmake
```
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local
```
output
```
-- JRL cmakemodules found in 'cmake/' git submodule
-- Configuring "pinocchio" (http://github.com/stack-of-tasks/pinocchio)
-- Package version (ROS package.xml): 3.6.0
-- Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 
-- Failed to find Doxygen, documentation will not be generated.
-- Default C++ standard: 201402
-- C++ standard sufficient: Minimal required 11, currently defined: 14
-- CMAKE_CXX_STANDARD was not set: automatically set to currently defined standard 14
-- Template instantiation of the main library
-- C++ standard sufficient: Minimal required 11, currently defined: 14
-- Since urdfdom >= 1.0.0, the default C++ standard is C++11. The project is then compiled with C++11 standard.
-- C++ standard sufficient: Minimal required 11, currently defined: 14
-- Since urdfdom >= 1.0.0, the default C++ standard is C++11. The project is then compiled with C++11 standard.
-- The Python bindings of Pinocchio will be compiled along the main library. If you want to disable this feature, please set the option BUILD_PYTHON_INTERFACE to OFF.
-- Checking for NumPy
--   NUMPY_INCLUDE_DIRS=/home/tars/system/miniconda3/envs/franka/lib/python3.8/site-packages/numpy/core/include
--   NUMPY_VERSION=1.24.4
-- PythonLibraryDirs: /home/tars/system/miniconda3/envs/franka/lib
-- PythonLibVersionString: 3.8.20
-- Python site lib: lib/python3.8/site-packages
-- Python include dirs: /home/tars/system/miniconda3/envs/franka/include/python3.8
-- Checking for NumPy
--   NUMPY_INCLUDE_DIRS=/home/tars/system/miniconda3/envs/franka/lib/python3.8/site-packages/numpy/core/include
--   NUMPY_VERSION=1.24.4
-- NumPy include dir: /home/tars/system/miniconda3/envs/franka/lib/python3.8/site-packages/numpy/core/include
-- eigenpy FOUND. eigenpy at /usr/local/lib/libeigenpy.so
-- Found Boost: /usr/include (found version "1.71.0") found components: python38 
-- C++ standard sufficient: Minimal required 11, currently defined: 14
-- Python compiler: CPython
-- Performing Test res_-Wno-conversion
-- Performing Test res_-Wno-conversion - Success
-- Performing Test res_-Wno-comment
-- Performing Test res_-Wno-comment - Success
-- Performing Test res_-Wno-self-assign-overloaded
-- Performing Test res_-Wno-self-assign-overloaded - Failed
-- Performing Test res_-Xclang=-fno-pch-timestamp
-- Performing Test res_-Xclang=-fno-pch-timestamp - Failed
-- Found Boost: /usr/include (found version "1.71.0") found components: unit_test_framework 
-- Valgrind not found, memory checks are disabled
-- Performing Test res_-Wno-maybe-uninitialized
-- Performing Test res_-Wno-maybe-uninitialized - Success
-- Performing Test res_-Wuse-after-free=0
-- Performing Test res_-Wuse-after-free=0 - Failed
-- Create files for AMENT (ROS 2)
-- Configuring done (1.6s)
-- Generating done (0.1s)
-- Build files have been written to: /home/tars/Franka/pinocchio/build
```
#### 3. make
```
sudo make -j4
```
output
```
[ 98%] Built target eigenpy-std_array
[100%] Linking CXX shared library ../lib/bind_virtual_factory.cpython-38-x86_64-linux-gnu.so
cd /home/tars/Franka/eigenpy/build/unittest && /usr/local/bin/cmake -E cmake_link_script CMakeFiles/eigenpy-bind_virtual_factory.dir/link.txt --verbose=1
/usr/bin/c++ -fPIC  -Wno-long-long -Wall -Wextra -Wcast-align -Wcast-qual -Wformat -Wwrite-strings -Wconversion  -shared -Wl,-soname,bind_virtual_factory.cpython-38-x86_64-linux-gnu.so -o ../lib/bind_virtual_factory.cpython-38-x86_64-linux-gnu.so "CMakeFiles/eigenpy-bind_virtual_factory.dir/bind_virtual_factory.cpp.o"  -Wl,-rpath,/home/tars/Franka/eigenpy/build/lib ../lib/libeigenpy.so /usr/lib/x86_64-linux-gnu/libboost_python38.so 
make[2]: 离开目录“/home/tars/Franka/eigenpy/build”
[100%] Built target eigenpy-bind_optional_boost
make[2]: 离开目录“/home/tars/Franka/eigenpy/build”
[100%] Built target eigenpy-bind_virtual_factory
make[1]: 离开目录“/home/tars/Franka/eigenpy/build”
/usr/local/bin/cmake -E cmake_progress_start /home/tars/Franka/eigenpy/build/CMakeFiles 0
```
#### 4.install
```
sudo make install
```
output
```
...
-- Up-to-date: /usr/local/include/eigenpy/config.hpp
-- Up-to-date: /usr/local/include/eigenpy/deprecated.hpp
-- Up-to-date: /usr/local/include/eigenpy/warning.hpp
-- Installing: /usr/local/share/ament_index/resource_index/packages/eigenpy
-- Installing: /usr/local/share/eigenpy/hook/ament_prefix_path.dsv
-- Installing: /usr/local/share/eigenpy/hook/python_path.dsv
-- Installing: /usr/local/share/eigenpy/package.xml
-- Installing: /usr/local/lib/cmake/eigenpy/cxx-standard.cmake
-- Installing: /usr/local/lib/cmake/eigenpy/eigenpyConfig.cmake
-- Installing: /usr/local/lib/cmake/eigenpy/eigenpyConfigVersion.cmake
-- Installing: /usr/local/lib/cmake/eigenpy/eigenpyTargets.cmake
-- Installing: /usr/local/lib/cmake/eigenpy/eigenpyTargets-noconfig.cmake
```
# reference：
https://blog.csdn.net/HH_Bang/article/details/139702662