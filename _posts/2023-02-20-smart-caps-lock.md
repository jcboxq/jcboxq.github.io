---
title: Smart Caps Lock and Smart Input Method for Vim
tags: Vim 按键绑定 输入法智能切换
mathjax: true
---

## 问题描述
使用 Vim 时想按 Esc 或者 Ctrl 很烦；中文输入时也很烦，需要在不同模式下频繁切换输入法；本文全都解决！
<!--more-->

## Smart Caps Lock 
Esc 和 Ctrl 很难按，最优解法是把没用的 Caps Lock 键映射成如下规则：按一下相当于 Esc；和其他键一起按下相当于 Ctrl。通过 AutoHotKey 实现，参考源:
1. [tanyuan's gist](https://gist.github.com/tanyuan/55bca522bf50363ae4573d4bdcf06e2e)
1. [youtube video](https://www.youtube.com/watch?v=fSfuHspXy5s)

## Smart Input Method 
用 vim 输入中文时需要在不同模式下切换输入法，最优解法是在切换模式时自动切换系统的输入法，这件事 vim 本身好像就可以设置（:help iminsert），但是看了半天感觉设置起来很麻烦，然后看到 [vscodevim 文档](https://github.com/VSCodeVim/Vim#input-method)里介绍了自己的 Input Method 自动切换实现，按照其方法设置后实现了输入法的自动切换。最后，还在`window设置`中搜索开启了`允许我为每个应用窗口使用不同的输入法`，这样系统就会记住不同窗口中采用的输入法（以及对应的中英状态），更减少了输入法切换的次数。