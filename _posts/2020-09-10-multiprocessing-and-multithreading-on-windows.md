---
title:  Multiprocessing and Multithreading on Windows
tags: 操作系统
---
# 问题描述
Debug过程中遇到**pickle.PicklingError: Can't pickle**
# 原因
在Windows中，多进程使用的是序列化pickle在多进程之间转移数据，而很多对象是不能被序列化的，但是在linux操作系统上却没问题，因为在linux上多进程使用的是fork。
# 解决办法
改用多线程。