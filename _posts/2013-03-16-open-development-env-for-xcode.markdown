---
layout: post
title: "open-development-env-for-xcode"
date: 2013-03-16 20:40
comments: true
categories: sortedapp iphone-dev
---

发现一个问题，使用theos这个makefile工具做app有很大困难，就是headers不好管理，真希望能集成到xcode中开发tweak，结果发现了一个神器----iOSOpenDev。

安装好之后就能发现xcode中已经有很多可用的template了，对于tweak来说，有logos和CaptaionHook。logos就是theos，captainhook是另一个hook框架。

不过很可惜，可能是sdk6.1的问题，结合上springboard和uialertview后就从来没build success，总说armv7中的springboard link error或者uialertview linker error，是在不知道怎么办了，仔细又看了别人的做法，发现他们还在用sdk5.1，估计就是这点差异吧？

彻夜下载sdk5.1.。。。。。。
