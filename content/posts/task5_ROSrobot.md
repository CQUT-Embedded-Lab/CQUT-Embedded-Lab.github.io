+++
author = "causehhc"
title = "任务书5—ROS机器人基础"
date = "2021-09-13"
description = ""
tags = ["stm32", "ROS-melodic", "Ubuntu18.04"]
categories = ["LabTask"]
+++

# ROS机器人任务书
![image](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913163548.jpg)
## 一、任务书
### 1、任务描述
- 搭建基础ROS环境，实现**数据**与**视频**传输
- 参考资料：
    - [AUTOLABOR资料](http://www.autolabor.com.cn/book/ROSTutorials/)
### 2、要求
- Ubuntu版本：18.04，ROS版本：melodic
- 实现机器人与数据与视频传输
- 调用接口实现基于激光雷达的SLAM
### 3、完成时间
- 1-2周
## 二、具体计划
### 1、阶段1
#### 1.1、工作安排
- 搭建Ubuntu虚拟机及ROS环境
- 参考资料：
    - 虚拟机安装流程：略
    - [ROS-melodic官方安装流程](http://wiki.ros.org/melodic/Installation/Ubuntu)
    - [HelloWorld例程](http://www.autolabor.com.cn/book/ROSTutorials/chapter1/13-rosji-cheng-kai-fa-huan-jing-da-jian.html)
#### 1.2、期望结果
- 使用VMWarePlayer与Ubuntu18.04镜像，搭建虚拟机环境
- 在Ubuntu18.04上搭建ROS-melodic系统
- 实现HelloWorld例程
#### 1.3、建议完成时间
- +1day
### 2、阶段2
#### 2.1、工作安排
- 了解ROS架构及文件系统
#### 2.2、期望结果
- [参考资料第一章](http://www.autolabor.com.cn/book/ROSTutorials/chapter1.html)
#### 2.3、建议完成时间
- +2day
### 3、阶段3
#### 3.1、工作安排
- 掌握Pub与Sub的通信模式，实现数据传输
#### 3.2、期望结果
- [参考资料第二章](http://www.autolabor.com.cn/book/ROSTutorials/di-2-zhang-ros-jia-gou-she-ji.html)
#### 3.3、建议完成时间
- +3day
### 4、阶段4
#### 4.1、工作安排
- 了解usb_cam包，实现视频传输
#### 4.2、期望结果
- 了解usb_cam发布的N种话题及其区别
- 使用rosrun image_view观察图像
- 使用rostopic测试各节点带宽
#### 4.3、建议完成时间
- +4day
### 5、阶段5
#### 5.1、工作安排
- 了解ROS多机通信，实现内网环境下的ROS配置
#### 5.2、期望结果
- 为树莓派安装Ubuntu18.04及ROS-melodic系统
- 完成ROS-Master等配置
- 实现主机与子机的通信
#### 5.3、建议完成时间
- +5day
### 6、阶段6
#### 6.1、工作安排
- 查找相关资料，实现基于激光雷达的SLAM
#### 6.2、期望结果
- 了解实验室现存激光雷达的型号
- 下载相应的pkg，并运行例程
- 输出模拟图像
#### 6.3、建议完成时间
- +6day
### 7、阶段7
#### 7.1、工作安排
- 总结项目
#### 7.2、期望结果
- 输出技术文档一份
#### 7.3、建议完成时间
- +7day
