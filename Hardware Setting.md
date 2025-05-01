# Hardware Setting
## Install Tutorial
## [video](https://www.bilibili.com/video/BV1U6vNeCExe/?spm_id_from=888.80997.embed_other.whitelist&bvid=BV1U6vNeCExe&vd_source=f65938b935c55207f67b4be1aaaf9b29)

## Equipment Overview
<img src="img/16.png" width="70%"/>

<img src="img/17.png" width="70%"/>

## Real-world Install overview

<img src="img/18.png" width="70%"/>

<img src="img/19.png" width="70%"/>

<img src="img/20.png" width="70%"/>

## Gripper Install
<img src="img/21.png" width="70%"/>

<img src="img/22.png" width="70%"/>

<img src="img/23.png" width="70%"/>

<img src="img/24.png" width="70%"/>

安装`gripper`时，定位硝也要安装，来减少固定误差，夹爪连线口上有白色的线，夹爪口白线对应机械臂末端接口白线处，然后插进即可

# Desk Control
## Start
按控制箱上的按钮进行开机，等待`30s`左右机械臂上的灯会变为蓝色

`ATTENTION`: 如果控制器上的灯为红色，则可能是按了急停

## ip address setting
用网线连接机械臂底座和电脑

<img src="img/25.png" width="70%"/>

<img src="img/26.png" width="70%"/>

机械臂ip地址：`192.168.0.1`

PC地址：`192.168.0.2`

<img src="img/27.png" width="70%"/>

<img src="img/28.png" width="70%"/>

输入`ip`地址后点击应用

然后在终端查看`ip`

```
ifconfig
```

<img src="img/29.png" width="70%"/>

可以看到此时地址已经改为了设置的地址，之后通过`website`进行控制

## website 
`ATTENTION`: 这里不能使用VPN，否则可能连接不上

打开浏览器，使用`chrome`或`firefox`，在浏览器中输入`192.168.0.1`后弹出登陆界面

<img src="img/30.png" width="70%"/>

### account
admin用户名：`franka`

密码：`franka123`

safetyOperator用户名：`franka_so`

密码：`franka123`

+ admin VS safetyOperator
    + 1. `safetyOperator`可以修改安全规则，而`admin`不可以
    + 2. `admin`功能更全

登陆后界面

<img src="img/31.png" width="70%"/>

<img src="img/32.png" width="70%"/>

然后先解锁，会听到咔咔的关节解锁声音，然后就变成以下状态

<img src="img/33.png" width="70%"/>

## Gripper
### 已有默认配置

<img src="img/34.png" width="70%"/>

<img src="img/35.png" width="70%"/>

开始红框里的夹爪不显示为激活状态，要点击红框，然后在右边的页面里点击`activate`

### 无默认配置
添加配置，并选择为`Franka Hand`模式，并点击保存
<img src="img/36.png" width="70%"/>

<img src="img/37.png" width="70%"/>

而后点击`ACTIVATE`

<img src="img/38.png" width="70%"/>

<img src="img/39.png" width="70%"/>

点击后`gripper`显示为`Activate`状态，在`SETTINGS/Dashboard`中`Franka Hand`显示为`uninitalized`状态

<img src="img/40.png" width="70%"/>

而后回到`desk`页面

<img src="img/41.png" width="70%"/>

切换到红框的`End-Effector`页面中，点击`Re-initiate`进行连接
之后可以在`settings`页面中`Dashboard`里看到`Franka Hand`的状态为`Initialized`

<img src="img/42.png" width="70%"/>

### gripper control

<img src="img/43.png" width="70%"/>

在此模式下进行gripper control
机械臂末端上的上下左右按键，长按实现：
上：夹爪加紧
下：夹爪松开
左/右：控制夹爪位置

<img src="img/46.png" width="70%"/>

<img src='img/franka gripper.gif'>

## teach mode

<img src="img/44.png" width="70%" height="70%"/>

`Teach mode`只在`Programming`模式下有效

<img src='img/teach mode.gif'>

同样此模式下，`Pilot Mode`两种模式都可以，按住末端的2个按钮（轻按）即可自由移动

## pilot

<img src="img/45.png" width="70%"/>
