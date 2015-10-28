---
layout: post
title: "daemon-in-nginx"
date: 2014-01-06 21:57:39 +0800
comments: true
categories: bnly
---

最近要把bnly重新运行起来，前两天整理了cli版本的程序，放到[https://github.com/dawncold/bnly-cli](GitHub)，另一个web版的放到了bitbucket上的私有仓库，准备做部署的时候用，没想到bitbucket最近没有被kill，难道放开了？

用supervisor做进程管理的时候被nginx坑了，由于nginx的配置很强大，现在还处在搭建环境的初期，很多配置写不完整，导致了nginx总是在频繁启动，log中看到的是80端口已经被占用。。。找了半天只有nginx占着80，而且又不会开多个nginx（supervisor的配置中没有明确说开多个程序，默认一个），搜了挺长时间都没有结果。

突然想到了daemon。

nginx的文档建议生产环境应该off，但这个和我遇到的问题无关。默认daemon开了，supervisor运行后会认为nginx退出了，再启动一个，其实上一个已经启动成功，所以就总看到80端口被占用，于是在nginx的配置上加`deamon off`即可。

是不是很坑？