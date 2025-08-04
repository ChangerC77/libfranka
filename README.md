# Reading Order (very important !!!)
1. [Hardware Setting](https://github.com/ChangerC77/libfranka/blob/fr3/Hardware%20Setting.md)
2. [real-time kernal](https://github.com/ChangerC77/libfranka/blob/dev/real-time%20kernal.md)
> Before you using `Franka FCI`, you `MUST` set up `real-time kernal` first, because `real-time kernal` will make sure that the rate of control reaches 1kHz without delay. see more details in `real-time kernal.md`

3. libfranka.md (current markdown)
4. [franka-interface](https://github.com/ChangerC77/franka-interface)
5. [frankapy](https://github.com/ChangerC77/frankapy)

# libfranka
## official reference: 
https://github.com/frankaemika/libfranka/blob/main/README.md
https://frankaemika.github.io/docs/libfranka.html

## API:
https://frankaemika.github.io/libfranka/0.15.0/

## 1. Installing dependencies
```
sudo apt-get update
sudo apt-get install -y build-essential cmake git libpoco-dev libeigen3-dev libfmt-dev
```
To use libfranka version `0.14.0` or later, you will need to install `pinocchio` and some more dependencies:

### system version: 
according to our `Robot/Gripper Server is 9`, so here we use `0.15.0` version, 

<img src='img/5.png' width='70%'>

`ubuntu20.04(noetic), franka_ros(0.10.0), libfranka (0.15.0)`

```
sudo apt-get install -y lsb-release curl
sudo mkdir -p /etc/apt/keyrings
curl -fsSL http://robotpkg.openrobots.org/packages/debian/robotpkg.asc | sudo tee /etc/apt/keyrings/robotpkg.asc
```
output
```
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
lsb-release 已经是最新版 (11.1.0ubuntu2)。
curl 已经是最新版 (7.68.0-1ubuntu2.25)。
下列软件包是自动安装的并且现在不需要了：
  gir1.2-goa-1.0 libfwupdplugin1 libncurses5 libtinfo5 libxmlb1
  linux-headers-5.11.0-27-generic linux-hwe-5.11-headers-5.11.0-27
  linux-image-5.11.0-27-generic linux-modules-5.11.0-27-generic
  linux-modules-extra-5.11.0-27-generic
使用'sudo apt autoremove'来卸载它(它们)。
升级了 0 个软件包，新安装了 0 个软件包，要卸载 0 个软件包，有 2 个软件包未被升级。
-----BEGIN PGP PUBLIC KEY BLOCK-----

...
-----END PGP PUBLIC KEY BLOCK-----
```
then
```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/robotpkg.asc] http://robotpkg.openrobots.org/packages/debian/pub $(lsb_release -cs) robotpkg" | sudo tee /etc/apt/sources.list.d/robotpkg.list
```
```
sudo apt-get update
sudo apt-get install -y robotpkg-pinocchio
```
if you install `pinocchio` failed, you can follow this tutorials `pinocchio`


## 2. Building and Installation from Source
Before building and installing from source, please uninstall existing installations of libfranka to avoid conflicts:
```
sudo apt-get remove "*libfranka*"
```
output
```
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
注意，根据Glob '*libfranka*' 选中了 'robotpkg-libfranka'
注意，根据Glob '*libfranka*' 选中了 'ros-foxy-libfranka-dbgsym'
注意，根据Glob '*libfranka*' 选中了 'robotpkg-libfranka+doc'
注意，根据Glob '*libfranka*' 选中了 'ros-foxy-libfranka'
注意，根据Glob '*libfranka*' 选中了 'ros-noetic-libfranka'
注意，根据Glob '*libfranka*' 选中了 'ros-noetic-libfranka-dbgsym'
软件包 robotpkg-libfranka+doc 未安装，所以不会被卸载
软件包 robotpkg-libfranka 未安装，所以不会被卸载
软件包 ros-noetic-libfranka 未安装，所以不会被卸载
软件包 ros-noetic-libfranka-dbgsym 未安装，所以不会被卸载
软件包 ros-foxy-libfranka 未安装，所以不会被卸载
软件包 ros-foxy-libfranka-dbgsym 未安装，所以不会被卸载
下列软件包是自动安装的并且现在不需要了：
  gir1.2-goa-1.0 libfwupdplugin1 libncurses5 libtinfo5 libxmlb1
  linux-headers-5.11.0-27-generic linux-hwe-5.11-headers-5.11.0-27
  linux-image-5.11.0-27-generic linux-modules-5.11.0-27-generic
  linux-modules-extra-5.11.0-27-generic
使用'sudo apt autoremove'来卸载它(它们)。
升级了 0 个软件包，新安装了 0 个软件包，要卸载 0 个软件包，有 2 个软件包未被升级。
```
### Clone the Repository
You can clone the repository and choose the version you need by selecting a specific tag:
```
cd ~/Franka
git clone --recurse-submodules https://github.com/ChangerC77/libfranka.git
cd libfranka
```
List available tags
```
git tag -l
```
Checkout a specific tag (e.g., `fr3 = 0.15.0`)
```
git checkout fr3
```
update submodules
```
git submodule update
```
Create a build directory and navigate to it
```
mkdir build
cd build
```
Configure the project and build
```
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=/opt/openrobots/lib/cmake -DBUILD_TESTS=OFF ..
make
```
output
```
[ 92%] Linking CXX executable motion_with_control_external_control_loop
[ 92%] Built target motion_with_control_external_control_loop
[ 93%] Building CXX object examples/CMakeFiles/print_joint_poses.dir/print_joint_poses.cpp.o
[ 94%] Linking CXX executable print_joint_poses
[ 94%] Built target print_joint_poses
[ 96%] Building CXX object examples/CMakeFiles/vacuum_object.dir/vacuum_object.cpp.o
[ 97%] Linking CXX executable vacuum_object
[ 97%] Built target vacuum_object
[ 98%] Building CXX object examples/utility_examples/CMakeFiles/logging_example.dir/logging_example.cpp.o
[100%] Linking CXX executable logging_example
[100%] Built target logging_example
```
### Installing libfranka as a Debian Package (Optional but recommended)
Building a Debian package is optional but recommended for easier installation and management. In the build folder, execute:
```
cpack -G DEB
```
output
```
CPack: Create package using DEB
CPack: Install projects
CPack: - Run preinstall target for: libfranka
CPack: - Install project: libfranka []
CPack: Create package
CPack: - package: /home/tars/Franka/libfranka/build/libfranka-0.15.0-x86_64.deb generated.
```
This command creates a Debian package named libfranka--.deb. You can then install it with:
```
sudo dpkg -i libfranka*.deb
```
`you can find this deb file in our code`

Installing via a Debian package simplifies the process compared to building from source every time. Additionally the package integrates better with system tools and package managers, which can help manage updates and dependencies more effectively.

## 3. connect
首先用网线连接机械臂底座和电脑，然后通过连接机械臂底座进入Desk设置控制器的ip地址

`ATTENTION`: 机械臂底座ip和控制器ip不能在同一域名下
- 机械臂底座连接模式下

    + `机械臂底座ip`: 192.168.0.1   
    + `本机ip`: 192.168.0.2

- FCI模式下

    + `控制器ip`: 192.168.1.10     
    + `本机ip`: 192.168.1.6

<img src='img/6.png'>
点击apply设置
<img src='img/7.png'>

设置好后，拔掉和机械臂底座的网线连接，拿网线和控制器网口相连

`检查好网线，有些细的网线不能用，实测粗的网线可以用`

有线网络设置：在`设置/网络/有线`中添加`有线ip地址`

<div style="display: flex; justify-content: space-around; width: 80%">
    <img src='img/8.png'>
    <img src='img/9.png'>
</div>

设置后可以在Dashboard中查看

<img src='img/10.png'>

## 4. website设置
在页面中`Activate FCI`，激活后可以在`SETTINGS/System/Installed Features`看到`FCI`

<div style="display: flex; justify-content: space-around; width: 80%;">
    <img src='img/11.png'> 
    <img src='img/12.png'>
</div>

## 5. Control

<div style="display: flex; justify-content: space-around; width: 80%;">
  <img src="img/13.png">
  <img src="img/14.png">
  <img src="img/15.png">
</div>

在`FCI`激活后，在`Execution`状态可以实现代码控制
```
cd ~/Franka/libfranka/build/examples
```
### 机器人回到home state
```
./communication_test 192.168.1.10
```
### 输出机器人状态
```
./echo_robot_state 192.168.1.10
```
### 机器人关节状态
获取机器人各joint相对于base frame的transform matrix
```
./print_joint_poses 192.168.1.10
```
在参数中找到q的参数
`"q": [0.0274532,-0.296549,0.20926,-2.37963,0.0801048,1.79244,0.791906],`
### 关节角度控制
```
./joint_point_to_point_motion 192.168.1.10 0.0274532 -0.296549 0.20926 -2.37963 0.0801048 1.79244 0.791906 0.1
```
最后一个是速度比例，一个参数不代表每个关节的速度一样
### 肘部运动
```
./generate_elbow_motion 192.168.1.10
```
肘部不动，关节动
### 阻抗控制
```
./cartesian_impedance_control 192.168.1.10
```
不是无节制柔性，顶得越厉害，阻碍越大，但其实回不到初始位置，阻尼会有能量损耗
### 夹爪控制
```
./grasp_object 192.168.1.10 1 0.01
```

### bug
可能会报错：
```
libfranka: unable to set realtime scheduling: Operation not permitted
```
这时控制要进入root模式
```
sudo passwd root
```
output
```
新的 密码： 
重新输入新的 密码： 
passwd：已成功更新密码
```
then, step in `su`
```
su
```