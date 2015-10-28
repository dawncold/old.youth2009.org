---
layout: post
title: putty的中文乱码
comments: true
date: 2012-03-02 12:08
categories: dev
---

着急回家就没带mbp，现在需要修改一下服务器上的文件，于是用了putty这款软件，一定要去官方下载啊，记得前一段时间爆发了在putty中嵌入木马从而盗取了N多服务器的root权限事件。

不过在用的时候发现查看带有中文字符的文件会出现乱码，在这里得到了解决方案：

0. 打开putty主程序，选择window-〉Appearance-〉Font settings-〉Change…,选择Fixedsys字体,字符集选择CHINESEGB2312。 

1. 在window-〉Appearance -〉Translation中，Received data assumed to be in which character set 中,把Use font encoding改为UTF-8如果经常使用,把这些设置保存在session里面. 

2. 现在打开putty,登录成功后,在shell中输入:export LCALL=’zh_CN.utf8’ 

然后再打开文件就没问题了。