---
layout: post
title: "big-break-in-tweak-app-build"
date: 2013-03-17 09:15
comments: true
categories: sortedapp iphone-dev
---

昨晚弄到1点多也没搞定iOSOpenDev，总是编译出问题，在irc上问了一下也没人回答我，看来还是有很多人在泡irc的！

睡前又看了一下各种文章，等起床打算还是回归theos搞搞试试。

没想到早晨用theos搞了一下竟然ok了！或许是用对了theos的版本？不清楚了。

theos我删掉了原来的，用github上的版本

{% codeblock lang:bash %}
git clone git://github.com/DHowett/theos.git $THEOS
{% endcodeblock %}

ldid我自己编译的，因为dropbox上的总是很难下载

{% codeblock lang:bash %}
git clone git://git.saurik.com/ldid.git
cd ldid
git submodule update --init
./make.sh
cp -f ./ldid $THEOS/bin/ldid
{% endcodeblock %}

有篇教程说在iOS上也安装perl和theos，我实在不清楚有什么用，不过我也安装了，蛋疼，具体方法看[这里](http://iphonedevwiki.net/index.php/Theos/Getting_Started)

headers用这里的：[https://github.com/rpetrich/iphoneheaders](https://github.com/rpetrich/iphoneheaders)需要注意一点的是IOSurface这个framework，你需要增加一个新的头文件，在Mac系统中，可能还得注释掉两行，这取决于你是不是10.7版本的Mac系统。命令是：`cp /System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h .`，在251和255行（我编译错误时候提示的就这两行），注释掉

{% codeblock %}
/* This call lets you get an xpc_object_t that holds a reference to the IOSurface.
  Note: Any live XPC objects created from an IOSurfaceRef implicity increase the IOSurface's global use
  count by one until the object is destroyed. */
//xpc_object_t IOSurfaceCreateXPCObject(IOSurfaceRef aSurface)
//IOSFC_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);


/* This call lets you take an xpc_object_t created via IOSurfaceCreatePort() and recreate an IOSurfaceRef from it. */
//IOSurfaceRef IOSurfaceLookupFromXPCObject(xpc_object_t xobj)
//IOSFC_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
{% endcodeblock %}

然后做你的tweak就可以了，我按照经典的heloworld例子搞了个hook，springboard中applicationDidFinishLaunching弹出alert，成功了。

OS:10.8.3，SDKVERSION：6.1

另外昨天说的设置theos的环境变量，我今天又重新加到了bash_profile中，发现make package install都能自动部署了。。。看来真是昨天theos版本的问题？！
