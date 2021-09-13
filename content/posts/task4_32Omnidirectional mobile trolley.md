+++
author = "causehhc"
title = "任务书4—32全向移动小车"
date = "2021-09-13"
description = ""
tags = ["stm32", "Omnidirectional", "TCP/IP", "Python"]
categories = ["LabTask"]
+++

# 32全向移动小车任务书
![image](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913162339.jpg)
## 一、任务书
### 1、任务描述
- 实现32小车的全向移动控制，可以通过串口向小车发出控制指令
- 相关资料（**不建议刚开始就看源码**）：
    - [stm32底盘驱动](https://github.com/CQUT-Embedded-Lab/stm32driver)
    - [多线程C/S模型(Socket)](https://github.com/CQUT-Embedded-Lab/Socket_CSModel)
    - [Python+ESP8266+stm32数据传输](https://github.com/CQUT-Embedded-Lab/Flask-stm32-dataTrans)
    - [使用frp实现内网穿透](https://causehhc.github.io/2021/04/use-frp-to-achieve-intranet-penetration/)
### 2、要求
- 掌握直流编码电机的控制与调速方法
- 实现闭环控制模型：增量式PI控制器
- 实现麦克纳姆轮的全向移动运动学建模
- 实现通过串口向小车发出控制指令
- 理解TCP/IP通信原理，使用pyhton-socket实现与esp8266的网络通信
- 实现局域网控制小车的全向移动
### 3、完成时间
- 1-2周
## 二、具体计划
### 1、阶段1
#### 1.1、工作安排
- 驱动直流电机转动
#### 1.2、期望结果
- 了解L289N的工作原理
- 尝试直接对L298N供电使直流电机转动
- 掌握直流电机的正转与反转
#### 1.3、建议完成时间
- +1day
### 2、阶段2
#### 2.1、工作安排
- 直流电机的PWM调速
#### 2.2、期望结果
- 理解PWM及用于直流电机调速的原理
- 利用stm32输出PWM，并通过示波器观察波形
- 将stm32输出的PWM接入L298N，并使其驱动电机
- 通过改变PWM占空比实现电机调速
#### 2.3、建议完成时间
- +2day
### 3、阶段3
#### 3.1、工作安排
- 直流电机闭环控制
#### 3.2、期望结果
- 了解为什么要闭环控制及其基本原理
- 了解直流编码电机中编码器的定义
- 使用stm32定时器中的输入捕获或编码器模式获取电机编码值
- 了解增量式PI控制器，利用编码值与PWM完成单个电机的闭环控制
#### 3.3、建议完成时间
- +3day
### 4、阶段4
#### 4.1、工作安排
- 全向移动运动学建模
#### 4.2、期望结果
- 输入x、y、z方向速度，输出4个电机各自的速度
- 将模型推广为绝对方向的控制
#### 4.3、建议完成时间
- +4day
### 5、阶段5（难点）
#### 5.1、工作安排
- 通过网络+串口的方式控制小车移动
#### 5.2、期望结果
- 制定串口通讯协议，例如`[, x, y, z, ]`，并实现
- 了解eps8266的原理与sta模式，并实现其与实验室内网的网络连接
- 学习源码[C/S模型（Socket）](https://github.com/CQUT-Embedded-Lab/Socket_CSModel)与[Python+ESP8266+stm32数据传输](https://github.com/CQUT-Embedded-Lab/Flask-stm32-dataTrans)，了解tcp网络通信基本过程
- Note：部分源码可能是基于FreeRTOS的设计，只关心某个任务即可
#### 5.3、建议完成时间
- +5day
### 6、阶段6
#### 6.1、工作安排
- 编写简单上位机程序，实现遥控
#### 6.2、期望结果
- 可以通过键盘输入控制小车移动
- 满足项目总体要求
#### 6.3、建议完成时间
- +6day
### 7、阶段7
#### 7.1、工作安排
- 总结项目
#### 7.2、期望结果
- 输出技术文档一份
#### 7.3、建议完成时间
- +7day
