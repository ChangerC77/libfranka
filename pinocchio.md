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
注意：因为我们需要的是`C++`库，所以不需要同时生成`Python`版本的编译文件所以在`Cmake`前，要修改`Pinocchio`中的`CmakeLists.txt`文件来关闭这个选项，将下面的`BUILD_PYTHON_INTERFACE`的`ON`改为`OFF`即可。
如果一开始没有关闭`BUILD_PYTHON_INTERFACE`，会在编译时在里面`python`文件下面报错。

#### --- OPTIONS ----------------------------------------
```
OPTION(BUILD_BENCHMARK "Build the benchmarks" OFF)
OPTION(BUILD_UTILS "Build the utils" OFF)
OPTION(BUILD_PYTHON_INTERFACE "Build the Python bindings" ON)
OPTION(BUILD_WITH_COMMIT_VERSION "Build libraries by setting specific commit version" OFF)
```
Cmake
```
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local
```
Make
```
make -j4
```
install
```
sudo make install
```
# reference：
https://blog.csdn.net/HH_Bang/article/details/139702662