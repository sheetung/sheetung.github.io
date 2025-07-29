# 虚拟机Ubuntu20配置px4相关环境

虚拟机安装px4环境配置
<!--more-->

[Ubuntu20 px4 与ego_planner_for_visual配置](Ubuntu20%20px4%20与ego_planner_for_visual配置.md)
### 安装和配置PX4

1. github clone源码，此处需要代理 [Linux 开启与关闭代理](../blog/Linux%20开启与关闭代理.md)
```sh
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

2. 成功后，进入文件夹继续下载组件
```
cd PX4-Autopilot/
git submodule update --init --recursive
bash ./Tools/setup/ubuntu.sh
# !!！reboot 重启机器
```

3. 测试编译px4
```sh
make px4_sitl_default gazebo
```

### 安装mavros
1. 编译成功显示gazebo后，退出。并安装mavros
```sh
sudo apt-get install ros-noetic-mavros*
```

2. 测试，并解决报错问题
```sh
roslaunch mavros px4.launch
# 报错解决
sudo /opt/ros/noetic/lib/mavros/install_geographiclib_datasets.sh
```
![](/assets/ubt20_px4/20241106090111521.png)

### 切换PX4版本
1. 成功后切换PX4版本至工程需要的版本
>我这里配置工程 [ego visual](https://gitee.com/gchasing/ego_geometry_control), 需要版本为**1.12.3**
```sh
git checkout v1.12.3
git submodule update --init --recursive
```

2. 安装jdk8, 并切换版本
```sh
sudo apt install openjdk-8-jdk
sudo update-alternatives --config java # 选择Java 8 的指令
rm -rf Tools/jMAVSim/out
```

3. 编译**jmavsim**
```sh
make clean
make px4_sitl_default jmavsim
```

### 安装QGC

根据官网提示安装 [QGC](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html)

auth: sheetung

---

> 作者: 西塘  
> URL: https://sheetung.github.io/ubt20_px4/  

