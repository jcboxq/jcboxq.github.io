---
title: 三维感知实现方式比较
tags: 3DV
mathjax: true
---

## 问题描述
帮老板做三维视觉主题的路演PPT，顺大便总结一下三维感知的常见实现方式
<!--more-->

## 三维感知常见实现方式
1. 激光雷达：
  * 按测距原理分类：三角测距(扫地机器人)、ToF(directToF(time、自动驾驶)/indirectToF(phase))

  ![lidar_1](/assets/images/lidar_1.png){:height="50%" width="50%"}

  * 按扫描方式分类：机械式、半固态（MEMS，旋镜式）、纯固态（OPA、Flash）。机械激光雷达带有控制激光发射角度的旋转部件，而固态激光雷达则无需机械旋转部件，主要依靠电子部件来控制激光发射角度。
2. ToF 相机：
  * 代表产品：Kinect 2.0

  ![kinect2](/assets/images/kinect2.png){:height="25%" width="25%"}
3. Structured Light(结构光相机)：
  * 代表产品：Kinect 1.0; iPhone X

  ![kinect1](/assets/images/kinect1.png){:height="25%" width="25%"}
4. Passive Stereo