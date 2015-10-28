---
layout: post
title: 分清form_for和form_tag
comments: true
date: 2012-02-14 19:34
categories: study ror
---

两个都是做form的指令，form_for是用来和一个model一块用的时候使用，form_tag就是普通的form了，侧重传值什么的。当初用了form_for来做了个登陆界面，怎么都得不到username和password，原来是这样，必须如此引用才可以——params[:user][:username]，前面的:user是我给form_for的第一个参数，这个form的所有信息都得加[:user]这样的前缀才能得到了，让我十分痛苦（又加上是个2.14）

使用form_tag后对于它的action不太会控制，所幸不写参数了，正好action指向本地址，省事儿！

感谢[这里](http://blog.csdn.net/babylon_0049/article/details/4730763)写的内容