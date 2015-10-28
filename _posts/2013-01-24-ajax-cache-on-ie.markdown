---
layout: post
title: "ajax cache on ie"
date: 2013-01-24 21:02
comments: true
categories: work@honovation
---

我们发现在IE浏览器中有些ajax操作表面看起来像是没有被执行一样，但手动刷新页面后发现真的执行过了刚刚的操作，进而发现在IE下ajax操作是有cache的。

hack的解决方法就是在request中加random参数，没啥实际效果，纯粹是不让cache出现而已。当然稍好一点的做法就是在jquery（我们是用jquery的）的$.ajax中加入参数{cache: false}即可。

如果你也遇到类似的效果，先看看是不是没有把cache写成false，默认是true的。
