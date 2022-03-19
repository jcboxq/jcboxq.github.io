---
title:  Login a Raspberry Pi for the First Time Without Monitor
tags: 树莓派
---
# 问题描述
从老师那里~~白嫖~~借用到一个树莓派却没钱买显示器，该怎么把玩它呢？
# 方法步骤
1. 在[官网](https://www.raspberrypi.org/downloads/)下载喜欢的系统镜像文件
2. 用镜像烧录软件（如balenaEtcher）将系统镜像烧录进 sd 卡
3. 进入 sd 卡的`boot`分区，创建文件名为`ssh`的无后缀文件，这一步的目的是开启树莓派的 ssh server 服务
4. 将 sd 卡插入树莓派
5. 让树莓派接入局域网，并获取它的 ip 地址
  * 如果拿到的树莓派**没有** WiFi 模块，直接使用网线连接树莓派和局域网路由器，web 访问路由器，查看 DHCP 客户端列表获取树莓派 ip 地址
  * 如果拿到的树莓派**有** WiFi 模块，除了网线直连路由器还可以修改 sd 卡上的`/etc/wpa_supplicant/wpa_supplicant.conf`配置文件，做到上电自动连接指定 WiFi，获取 ip 地址的方法同上
6. ssh 登录树莓派，`ssh pi@ip_address`，初始密码`raspberry`