---
layout: post
title: "build hybla for ubuntu 14.04"
date: 2015-10-27 00:42:28 +0800
comments: true
categories: study
---
When I modify some ipv4 config for system I got an error like this: `sysctl: setting key "net.ipv4.tcp_congestion_control": No such file or directory`, so I followed [this post](http://v2ex.com/t/114788) to build a kernel module for ubuntu 14.04

The net/ipv4 hybla Makefile(bad script format in original post):

```
# Makefile for tcp_hybla.ko
obj-m := tcp_hybla.o
KDIR := /home/dejavu/linux-4.1.5
PWD := $(shell pwd)
default:
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules
```

I also got a warning during build modules: `No X.509 certificates found`, but it doesn't matter I think, I can build the `tcp_hybla.ko` and load in kernel.