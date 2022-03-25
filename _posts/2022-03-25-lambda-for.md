---
title:  Python 中 lambda 和 for 一起使用时的坑
tags:  踩坑 Python CARLA
mathjax: true
---

## 问题描述
Python 中 lambda 和 for 一起使用时的坑
<!--more-->

## 有坑代码
```
    # 对 CARLA 中所有的 sensor 开始监听
    def begin_listen(sensor_list, sensor_queue, sensor_name_list):
        for i, sensor in enumerate(sensor_list):
            sensor.listen(lambda data: sensor_callback(data, sensor_queue, sensor_name_list[i]))
```
运行结果：所有 sensor 都被分配了同一个 sensor_name

## 正确代码
```
    # 对 CARLA 中所有的 sensor 开始监听
    def begin_listen(sensor_list, sensor_queue, sensor_name_list):
        for i, sensor in enumerate(sensor_list):
            sensor.listen(lambda data, i=i: sensor_callback(data, sensor_queue, sensor_name_list[i]))
```
坑点分析：要通过冒号前的 i=i 传入绑定随 for 变化的变量 i ，否则所有 lambda 表达式创建的函数都绑定的是变量 i 最后的值。