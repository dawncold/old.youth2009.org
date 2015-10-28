---
layout: post
title: "timestamp"
date: 2013-08-20 21:56
comments: true
categories: work@honovation
---

今天在做批量导入图片功能的时候，发现一个问题，原先save image过程用timestamp当文件名，这样在一般使用的时候倒是没什么问题了，但让程序去做的时候，timestamp就显得不好用了，程序跑的很快，可能三四张图都在1s内处理完上传，这样就很难保证文件名不重复。

传一张停1秒呢？问题不大，但看着还是不保险，而且变慢了，因为要等。。。

纯粹uuid倒是问题不大，但日后管理起来确实就不爽了——看uuid根本不知道谁先谁后，所以就把tiemstamp和uuid4连起来当新文件名，这样程序批量传也不会有问题（其实概率已经低到这个时代可接受的程度吧），又在trade off了。
