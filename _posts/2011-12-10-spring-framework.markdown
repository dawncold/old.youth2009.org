---
layout: post
title: Spring
comments: true
date: 2011-12-10 16:48
categories: S2SH
---

这不是代表春天或者温泉的意思，实际上是我正在学习期末考试课程S2SH中的一个框架——Spring。

就一变态框架啊，Ioc、AOP这些都是令业界震撼的思想级产物。特别是AOP，就是和OOP同层次的东西，怪不得学习起来很慢很艰难，不过我清楚，期末考试肯定考得超简单，现在我基本是学到哪里忘到哪里。

顺便说下，用Spring做一个简单的AOP测试实例的话，光用自带的jar包根本不行，还需要自己添加下面这几个：

1.aopalliance-1.0.jar（在struts2的lib目录中找到的）

2.aspcetjweaver-1.5.3.jar（aspcetj的官网怎么上都上不去：[http://www.aspectj.org](http://www.aspectj.org)，于是在这里下载的：[http://www.jar114.com/j/982](http://www.jar114.com/j/982)）

3.cglib-nodep-2.2.2.jar（本来用cglib-2.2.2.jar的，但提示缺少asm就下载了这个集成asm的nodep版本，我以为asm就是Spring中的那个asm包呢。官方网站：[http://cglib.sourceforge.net](http://cglib.sourceforge.net)）