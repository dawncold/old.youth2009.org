---
layout: post
title: 字符编码的问题
comments: true
date: 2011-01-18 08:36
categories: blog
---

昨日写完hello,world之后，发现里面的中文显示出来都是乱码，于是找了几处资料，先是怀疑emacs作怪，M-x describe-coding-system查看后挺正常，于是开始怀疑apache和php的输出编码，再次查询后也发现是正常的：httpd.conf中根本没有AddDefaultCharset” 内容，php.ini中的default_charset已经被注释掉了：（

于是开始怀疑网页编码，改成了：

{% codeblock lang:html %}
<meta content="text/html;charset = utf-8" http-equiv="Content-Type">
{% endcodeblock %}
（第一次我写成了mate！！！）这下已经正常了！


参考资料：[http://www.cnblogs.com/RChen/archive/2007/08/27/871427.html](http://www.cnblogs.com/RChen/archive/2007/08/27/871427.html)

在调节emacs和ibus的时候参考了[这里](http://www.sciencenet.cn/m/user_content.aspx?id=325692)，不过到现在我的ibus也不能在emacs中打开，除非用`LC_CTYPE=zh_CN.utf8 emacs`这样启动emacs。

感谢[这里](http://www.yzznl.cn/archives/242.html)下载了修改后的编辑界面和学习到了WP-Syntax的使用方法。