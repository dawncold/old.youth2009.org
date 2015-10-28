---
layout: post
title: "end-sorted"
date: 2013-03-18 22:10
comments: true
categories: sortedapp iphone-dev
---

暂时终止sorted的开发，经历了两天痛苦的、没白没黑的、浑浑噩噩的探索后，还是没能搞定iPhone上一个icon的移动过程。实在不行我都打算直接去修改iconstate.plist文件了。。。但就是修改了不能马上响应，需要respring这点受不了！

网上这方面的资料依然少的可怜，很多时间竟然是花在寻找headers文件了，最后才知道根本不需要。你只要有headers拿来看看就ok了，需要什么类的声明自己用@interface写在xm文件中就可以了。tweak的远离是做出dylib后加载，替代系统的api，headers文件对于你来说就是看，然后找需要哪些私有api即可。

过两天兴致来了或许又再搞一下。
