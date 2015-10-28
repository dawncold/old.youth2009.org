---
layout: post
title: 开启Dock的堆栈功能
comments: true
date: 2012-01-13 21:56
categories: mac
---

打开Terminal，输入：`defaults write com.apple.dock scroll-to-open -bool TRUE;killall Dock`

然后回车（return），等Dock再次出现后，在已打开程序图标上滚动鼠标滚轮或者手势模拟滚轮，就能看到这个程序打开的子窗口或者子程序，很过瘾好用。