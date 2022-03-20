---
title: Windows 上用 Python 跑并行计算
tags: 并行计算
---

## 问题描述
红外去反射项目需要用到并行计算，在 Windows 上利用多进程实现时遇到 **pickle.PicklingError: Can't pickle**

## 原因
在 Windows 上，需要使用序列化pickle在多进程之间转移数据，而很多对象是不能被序列化的，但是在 Linux 操作系统上却没问题，因为在 Linux 上多进程使用的是 fork.

## 解决办法
在 Windows 上改用多线程。