---
layout: post
title: struts2的eclipse提示
comments: true
date: 2011-12-01 14:32
categories: S2SH
---

写struts2的配置文件时如果有提示那最好了，添加方法比较简单，从框架的jar包中找到sruts-2.1.7.dtd文件，在preference搜索xml找到xml catalog，然后add一个，文件就是刚刚找到的dtd文件，Key type选URI，我用过publicID但没有提示效果，相应的，key中写：http://struts.apache.org/dtds/struts-2.0.dtd即可。