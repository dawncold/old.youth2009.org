---
layout: post
title: 最好在include_path中加上根
comments: true
date: 2011-07-09 16:54
categories: php
---

刚刚用了下typecho博客插件——友情链接来添加一个友情链接，但发现很多php文件找不到了，很奇怪，以前是可以的，看到warning中的信息，有个include_path的相关东西，看看里面提到的路径是不是有需要的文件，结果没有，而在其中路径的下一级目录下有，这就怪了。

Google说最好把include_path写成"./"。是不是这样就是自动便利所有的内容了？我猜是的！当前的include_path中又pear的路径，我就先不删除了，linux系统下用冒号分隔各个路径，在前面加上一个点即可。

重启php，再次访问，恢复正常！