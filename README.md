# **rslidar_sdk** 

# **V1.0.0**



---



### 1. 工程简介
  rslidar_sdk 为速腾聚创在Linux环境下的雷达驱动软件包，包括了雷达驱动内核， ROS拓展功能， Protobuf-UDP通信拓展功能。对于没有二次开发需求的用户，或是想直接使用ROS进行二次开发的用户，可直接使用本软件包， 配合ROS自带的RVIZ可视化工具即可查看点云。 对于有二次开发需求，想将雷达驱动集成到自己工程内的客户， 请参考雷达驱动内核的相关文档，直接使用内核进行二次开发。 



### 2. 下载

- 方法一 ------ 使用git clone

 由于rslidar_sdk项目中包含子模块驱动内核rs_driver, 因此在执行git clone 后还需要执行相关指令初始化并更新子模块。

```sh
git clone XXXX.git
cd rslidar_sdk
git submodule init
git submodule update
```

- 方法二 ------ 直接下载

由于直接下载的压缩包内不包含git信息，因此您需要手动下载驱动内核rs_driver(https://github.com/RoboSense-LiDAR/rs_driver), 然后将其解压在 rslidar_sdk/src/rs_driver路径下即可。





### 3. 依赖介绍

- ROS (若需在ROS环境下使用雷达驱动，则需安装ROS相关依赖库)

  安装方式： 参考 http://wiki.ros.org/kinetic/Installation/Ubuntu 

  **如果您安装了ROS kinetic desktop-full版，那么兼容版本的PCL，Boost，Eigen和OpenCV也应该同时被安装了，所以您不需要重新安装它们以避免多个版本冲突引起的问题,因此，强烈建议安装ROS kinetic desktop-full版，这将为您节省大量的时间来逐个安装和配置库**

- Eigen(必需, 若已安装ROS kinetic desktop-full, 可跳过)

- Boost(必需, 若已安装ROS kinetic desktop-full, 可跳过)

- PCL(必需, 若已安装ROS kinetic desktop-full, 可跳过)

- Protobuf (若需要使用Protobuf相关功能，则需安装Protobuf相关依赖库)

  安装方式:

  ```sh
  sudo apt-get install -y libprotobuf-dev protobuf-compiler
  ```

- pcap  (必需）

  安装方式：

  ```sh
  sudo apt-get install -y  libpcap-dev
  ```





### 4. 编译 & 运行

我们提供两种编译&运行方式

- 不依赖于ROS编译

  按照如下指令即可编译运行程序。 但需要用户在程序启动前手动启动roscore，启动后手动打开rviz。

```sh
    cd rslidar_sdk
    mkdir build && cd build
    cmake .. && make -j4
    ./rslidar_sdk_node
```

- 依赖于ROS编译

  - 打开工程内的*CMakeLists.txt*文件，将第三行的**set(ROS_COMPILE_SUPPORT false)**改为**set(ROS_COMPILE_SUPPORT true)**

    ```cmake
    cmake_minimum_required(VERSION 3.5)
    project(rslidar_sdk)
    set(ROS_COMPILE_SUPPORT true)
    ```

  - 新建一个文件夹作为工作空间，然后再新建一个名为*src*的文件夹, 将rslidar_sdk工程放入*src*文件夹内

  - 返回工作空间目录，执行以下命令即可编译&运行(若使用.zsh,将第二句指令替换为 *source devel/setup.zsh*)

    ```sh
    catkin_make
    source devel/setup.bash
    roslaunch rslidar_sdk start.launch 
    ```



### 5. 文件结构

|- config												*存放所有的参数文件*

|- demo												*存放node代码*

|- doc													*存放相关文档*

|- rviz													*存放rviz配置文件*

|- src													 *存放内核代码，以及ROS，Protobuf功能性代码*

|- CHANGELOG_CN.md					 

|- CHANGELOG_EN.md

|- CMakeLists.txt

|- README.md



### 6. 参数介绍

**参数介绍非常重要，请仔细阅读。 本软件包的所有功能都将通过改变参数来实现。**

[参数介绍](doc/intro/parameter_intro.md)



### 7. 快速上手

**以下仅为一些常用功能的快速使用指南， 实际使用时并不仅限于以下几种工作模式， 用户可通过配置参数改变不同的工作模式。**

[在线读取雷达数据发送到ROS](doc/howto/how_to_online_send_pointcloud_ros.md)

[录制ROS数据包&离线解析ROS数据包](doc/howto/how_to_record_and_offline_decode_rosbag.md)

[离线解析Pcap包发送到ROS](doc/howto/how_to_offline_decode_pcap.md)



### 8. 使用进阶

[隐藏参数介绍](doc/intro/hiding_parameters_intro.md)

[使用Protobuf发送&接收](doc/howto/how_to_use_protobuf_function.md)

[多雷达](doc/howto/how_to_use_multi_lidars.md)





---



### 1. Introduction

​	rslidar_sdk is the lidar driver software kit in Linux environment, which includes the driver core, ROS functional codes and Protobuf-UDP communication code. For users who want to use lidar driver through ROS, this software kit can be used directly. For users who want to do advanced development or integrate the lidar driver into their own projects, please refer to the lidar driver core. 



### 2. Download

- Method1 ------ Use git clone

Since rslidar_sdk project include the submodule --- rs_driver, user need to excute the following commands after git clone.

```sh
git clone XXXX.git
cd rslidar_sdk
git submodule init
git submodule update
```

- Method2 ------ Download directly

Since the zip file does not include submodule information, user need to download the driver core --- *rs_driver* manually (https://github.com/RoboSense-LiDAR/rs_driver). Then unzip the rs_driver under the path */rslidar_sdk/src/rs_driver*.



### 3. Dependencies

- ROS (If use rslidar_sdk in ROS environment, ROS related libraries need to be installed)

  Installation： please refer to  http://wiki.ros.org/kinetic/Installation/Ubuntu 

  **If you install ROS kinetic desktop-full，then the correspond PCL, Boost, Eigen and OpenCV will be installed at the same time. If will bring you a lot of convenience since you dont need to handle the version confliction. Thus, its highly recommanded to install ROS kinetic desktop-full**

- Eigen(Essential, if installed ROS kinetic desktop-full, this part can be ignored)

- Boost(Essential, if installed ROS kinetic desktop-full, this part can be ignored)

- PCL(Essential, if installed ROS kinetic desktop-full, this part can be ignored)

- Protobuf (If use Protobuf related functions, Protobuf need to be installed)

  Installation :

  ```sh
  sudo apt-get install -y libprotobuf-dev protobuf-compiler
  ```

- pcap (Essential)

  Installation：

  ```sh
  sudo apt-get install -y  libpcap-dev
  ```



### 4. Compile & Run

We offer two ways to compile and run the driver

- Compile with out ROS-catkin

  Excute the commands below. In this way, user need to start roscore before running the driver and need to start rviz manually.

```sh
    cd rslidar_sdk
    mkdir build && cd build
    cmake .. && make -j4
    ./rslidar_sdk_node
```

- Compile with ROS-catkin

  - Open the *CMakeLists.txt* in the project，modify the 3rd line **set(ROS_COMPILE_SUPPORT false)** to **set(ROS_COMPILE_SUPPORT true)**

    ```cmake
    cmake_minimum_required(VERSION 3.5)
    project(rslidar_sdk)
    set(ROS_COMPILE_SUPPORT true)
    ```

  - Create a new folder as the workspace, and create a *src* folder in the workspace. Then put the rslidar_sdk project in the *src* folder. 

  - Get to the workspace, excute the following command to compile and run. (if use .zsh, replace the 2nd command with *source devel/setup.zsh*)

    ```sh
    catkin_make
    source devel/setup.bash
    roslaunch rslidar_sdk start.launch 
    ```



### 5. File Structure

|- config												*Store all the configure files*

|- demo												*Store the code of running node* 

|- doc													*Store all the documents*

|- rviz													*Store the rviz configure file*

|- src													 *Store the lidar driver core, ROS related code and Protobuf-UDP related code*

|- CHANGELOG_CN.md					 

|- CHANGELOG_EN.md

|- CMakeLists.txt

|- README.md



### 6. Introduction to parameters

**This part is very important, please read carefully. All the functions of this software kit will be reach by modifying parameters.**

[Intro to parameters](doc/intro/parameter_intro.md)



### 7. Quick start

**The followings are some quick guides to using some of the most common features of the rslidar_sdk, but the software kit are not limited to the following modes of operation. Users can use rslidar_sdk in their own way by modifying parameters.**

[Online connect lidar and send pointcloud through ROS](doc/howto/how_to_online_send_pointcloud_ros.md)

[Record rosbag & Offline decode rosbag](doc/howto/how_to_record_and_offline_decode_rosbag.md)

[Decode pcap bag and send pointcloud through ROS](doc/howto/how_to_offline_decode_pcap.md)



### 8. Advanced

[Intro to hiding parameters](doc/intro/hiding_parameters_intro.md)

[Use protobuf send & receive](doc/howto/how_to_use_protobuf_function.md)

[Multi-LiDARs](doc/howto/how_to_use_multi_lidars.md)