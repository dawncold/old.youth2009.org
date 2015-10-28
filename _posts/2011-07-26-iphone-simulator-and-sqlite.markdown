---
layout: post
title: iphone模拟器和sqlite的问题
comments: true
date: 2011-07-26 09:19
categories: iphone-dev
---

最近和sqlite打交道比较频繁，感觉很别扭，可能是因为数据库的操作都在模拟器上测试的缘故吧，有几次查看数据库的内容总是没有结果，过一段时间就好了，我现在只能怀疑是模拟器搞的鬼。以后再弄数据库之前应该把模拟器中的程序删掉，重新传入数据。

今天update进去信息，总是没发现数据库更新，怀疑是忘记commit，查看一下FMDB的使用方法，确实有commit一说，而我在看国内某博客写的使用教程时发现他就是随意的update和insert，殊不知这些都需要commit呀！在update和insert代码前后需要加入


{% codeblock %}
[db beginTransaction];
和
[db commit];
{% endcodeblock %}

我用的Objective-C。

然而即便是这样，更新了数据库后再查询，确实数据被更改了，但我重新在模拟器中运行程序时候又恢复成了以前的值。偶然在模拟器中打开了程序而不是用xcode运行程序，数据竟然被永久更新了。

所以，以后测试update的时候，前后对比应该只在模拟器中看，如果再用xcode启动，会把原来的数据传入模拟器，这样你就看不到效果了。

