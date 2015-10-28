---
layout: post
title: VertexHelper的使用
comments: true
date: 2011-08-04 23:02
categories: gameapp iphone-dev
---

最近在用Box2d开发小游戏，不可避免用到多边形物体，当然有的形状还好描述，但大多数是那种难以描述的物体，所以这个VertexHelper就是不可或缺的武器了，它能够让你把需要的物体边界描出来，自动生成Box2d需要的边界代码。

没想到作者把软件放到app store上卖，但还提供源代码，不知道他们之间是什么不一样……

从GitHub那里得到源代码，打开xcode编译一下就能用了。

有一点需要说明，得到的源代码中Project的Base SDK是10.5，在我编译的时候提示了一个警告，现在找不到了。只需要把Target中VertexHelper的BaseSDK改为10.7就可以了，当然如果你没有10.7就只能用10.6了。可能是因为我没有10.5SDK才出现的错误吧。