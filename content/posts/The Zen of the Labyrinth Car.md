+++
author = "causehhc"
title = "迷宫小车之禅"
date = "2021-09-13"
description = ""
tags = ["C51"]
categories = ["嵌入式"]
+++

# 迷宫小车之禅

## 一、万事开头难

——绝对方向和相对方向

### 1、之前java迷宫移动一格

- 以坐标化的形式描述移动
- **[row, col]: [0, 0] -> [0, 1]**
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141526.jpg)

### 2、小车移动一格

- 以方向化的形式描述移动
- **[绝对方向]: 起始点 -> 前进一步**
- 在本例中，实现这种移动只需要使小车**前进**一步即可
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141532.jpg)

### 3、存在一个问题

- 小车的朝向似乎也是影响移动的因素
- **[绝对方向]：起始点 -> 右转90° -> 前进一步**
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141538.jpg)

### 4、问题的推广（相对方向的引出）

- 小车以任意起始方向存在于迷宫任意位置
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141541.jpg)
- 为方便表示，我们定义相对方向：
  - 0：直行
  - 1：右转
  - 2：掉头
  - 3：左转
- 得出迷宫移动的转换关系表
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141545.jpg)
- 可以观察到，起始方向与期望方向一致时，小车只需直行即可。但是当方向不一致的，首先需要调转小车的朝向，然后直行。
- 所以问题的重点就在于如何协调小车**第一步**的决策
  - 当然你可以把这16种情况直接写到程序中，每次判断即可
  - 但是这种情况存在一种计算公式

### 5、绝对方向 -> 相对方向的转换

- 定义

  - absD：起始方向（绝对方向）
  - absD_t：期望方向（绝对方向）
  - relD：小车相对方向

- 公式
  $$
  relD=(absD_t-absD)\pmod4
  $$

- 函数

```c
unsigned char abs_to_rel(unsigned char absD, unsigned char absD_t){
  //absD：当前绝对方向
  //absD_t：期望转换到哪个绝对方向
  unsigned char relD = (absD_t - absD) % 4;
  if(relD > 127)	relD += 4;
  //返回相对方向
  return relD;
}
```

### 6、使用案例

- 起始方向：1
- 期望方向：0
- relD = abs_to_rel(1, 0);
- 小车相对方向为3，执行左转，之后前进
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141551.jpg)

## 二、到底朝哪个方向走

——小车行进策略（遍历阶段）

### 1、只是为了走到终点

- “右手法则”，只适用于终点在边缘的迷宫
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141555.jpg)

### 2、遍历整个迷宫，延续之前java的思路

- 绝对方向从0->3扫描，一看到没墙就走，failed
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141559.jpg)
- 走过的路不应该再走，failed
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141612.jpg)
- 真没路的时候果断回溯
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141603.jpg)

### 3、明确判断策略

- 决定方向的两个依据
  - 是否有墙
  - 是否走过
- 4个方向都有墙或者都走过
  - 回溯

### 4、配合这种策略，最终它会回到起点，终于跑完了？

- 还有最优路径呢

## 三、爬山和下山

——基于BFS的最优路径查找

### 1、BFS过程

- ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141620.jpg)

```c
void bfs(){
  // step1：起点入队
  while(!isEmpty(queue)){
    // step2：a出队
    for(int i=0; i<4; i++){
      // step3：判断a周围的信息，依次入队
      // step4：刷新这个点的高度  
    }
    // step5：高度+1
  }
}
```

### 2、等高表

- ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141623.jpg)
- ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141628.jpg)

### 3、信息在哪？

- 需要在**遍历**的时候就收集好

## 四、内存吃紧，效率吃紧

——迷宫数组+栈、等高表+队列存储优化

### 1、迷宫数组+栈

#### 1.1、墙与路

- java迷宫，char数组，甚至是int数组（51内存不够）  
- ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141635.jpg)
- 更高效的存储方法
  - 一个char里面有些啥
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141638.jpg)
  - 可以用低4位表示一个格子墙的信息
- 例子（疯狂使用位运算）
  - `unsigned char block = 0b00001010;`
  - ![avatar](https://markdown-1305234562.cos.ap-chongqing.myqcloud.com/lab/2021/09/20210913141642.jpg)

#### 1.2、如何判断走过？如何确定回溯方向？

- 判断走过：把这个迷宫数组高四位置1
- 确定回溯方向：迷宫数组高四位直接存来的方向
- **双赢**

### 2、等高表+队列

- 你们可以尝试的优化点，我按老路子来的
  - 8*8等高表存高度
  - 长度64的缓存队列

## 五、总结

——一个简单的框架

```c
void proc(){
  while(1){
    // step1：刷新信息（方向转换+高低四位）
    // step2：确定方向（有没有墙+走没有过）
    // step3：开始执行（方向转换）
  }
}
```

