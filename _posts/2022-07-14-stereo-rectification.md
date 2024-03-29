---
title: 双目极线校正中的多解问题
tags: 3DV
mathjax: true
---

## 问题描述
双目极线校正存在多解，这是因为与基线垂直的光轴方向有无数条，那么实际求解校正矩阵时是如何解决这个问题的呢？
<!--more-->

## 双目极线校正大概流程
1. 通过双目标定/自标定获得双目内外参信息；

2. 根据平移向量计算左相机校正矩阵。这里可根据当前平移向量和校正后理想平移向量计算左相机坐标系的校正旋转矩阵。这里的转法有无数种（想像向量 A （当前平移向量）绕着向量 C （校正旋转向量）转到了向量 B （理想平移向量），C 只要在 A 和 B 的对称面上即可）。一种常用的 C（校正旋转向量）是方向由 A × B 确定，大小为 A 和 B 之间的夹角。

3. 校正双目图像时，左图根据 C（校正旋转向量）校正到位，右图先根据两相机之间的旋转向量校正到和原左相机坐标系无相对旋转，再根据 C（校正旋转向量）校正到位；