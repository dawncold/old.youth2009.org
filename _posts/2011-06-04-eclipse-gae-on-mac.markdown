---
layout: post
title: Mac系统下的Eclipse中GAE配置
comments: true
date: 2011-06-04 18:43
categories: python
---

用了不少时间PHP，也有些喜欢这种开发语言，但我仍然对Python有强烈的热情，但支持Python的主机服务还不算多，很想体验GAE，但由于在国内嘛，只能这样忍受了。

原本想在Emacs中配置Python的环境，但……有些过于复杂了。安装了很久的emacs，到头来不知道该怎么用，打算卸载掉算了，自己不需要的东西，不管它多么优秀，对于我来说，目前都没有价值！所以我还是选择了Eclipse环境。

在安装PyDev插件的时候遇到点问题：安装时候有3个项目可安装，我第一次是都安装的，但中途出现错误停止了，于是我第二次只安装了第一个，就是主要的PyDev程序，没有问题。

在创建一个GAE项目后，需要填写GAE的location，在Mac系统下，装了Google提供的SDK For Mac就找不到GAE的相关文件了，因为都在那个app包中，只是在/usr/local/bin中有几个相关的py文件，在/usr/local/中有个链接，链接到app包中的一个地方，主要就是用这个链接，不过你会发现这样用之后还有点问题，插件需要找到lib目录下的django，如果你看看目录的话会发现根本没有django目录，只有另一个叫django_0_96这样的目录，于是建立一个软连接到django过去即可。

以上方法来自国外一技术博客：
[http://www.joelennon.ie/2011/03/25/using-pydev-for-google-app-engine-development-on-a-mac](http://www.joelennon.ie/2011/03/25/using-pydev-for-google-app-engine-development-on-a-mac)