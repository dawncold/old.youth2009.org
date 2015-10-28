---
layout: post
title: jquery1.6+中的prop方法
comments: true
date: 2012-08-18 19:27
categories: js
---

最近有个网站需要一个简单的功能——全选一些checkbox，但用attr的方法总是出问题，主要问题如下：第一次全选没问题，如果此时取消选择一些checkbox，再用全选就不管用了，主要原因就是第一次全选的时候自动加入了checked属性，以后再强制attr("checked",true)就会没反应。在[这里](http://blog.csdn.net/yaerfeng/article/details/7792832)看到一篇文章，里面提到了prop方法，是1.6以后才加入的，就是部分替换了attr的功能，用了prop就可以及时对操作做出反应（这里我不太理解），总之本来用attr的操作现在需要用prop才有效果，当然了，如果你用纯js肯定是没问题喽。

换用prop之后，问题解决！

