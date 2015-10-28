---
layout: post
title: "build-up-env-for-sorted"
date: 2013-03-16 17:40
comments: true
categories: sortedapp iphone-dev
---

找到了一篇教程，开始构建jailbreaken app的环境。

基本需要的工具

{% codeblock lang:bash %}
export THEOS=/opt/theos
svn co http://svn.howett.net/svn/theos/trunk $THEOS
curl -s https://dl.dropboxusercontent.com/u/3157793/ldid > $THEOS/bin/ldid; chmod +x $THEOS/bin/ldid
brew install dpkg(如果出错安不上dpkg，那就先update一下brew，我就遇到这么个问题)
{% endcodeblock %}
用theos模板创建项目，`$THEOS/bin/nic.pl`，这会在当前目录中创建你的项目，选择模板类型，然后起名字之类的，填好就ok。

在创见出来的项目中有Makefile，里面有一个地方需要注意，就是`xxxx_FILES=`这里，后面的m和mm文件是你当前所有的，如果你自己加了新的，你需要手动添加进去。

再加两个环境变量

{% codeblock lang:bash %}
export SDKVERSION=6.1
export THEOS_DEVICE_IP=10.0.0.101
{% endcodeblock %}
目标sdk版本，我用6.1了，后一个是手机的ip，自己弄到一个wifi中吧，后面部署需要。

make&make package，在make的时候不加sudo我会无法make成功。

{% codeblock lang:bash %}
sudo make
sudo make package
{% endcodeblock %}
本目录下的deb就可以放到设备上安装了，安装命令是`dpkg -i xxx.deb`

不过你可以用部署的方式，`make package install`，他会依赖你刚刚设置的IP部署，但我这里似乎有问题，估计是环境变量的问题，光提示我找不到THEOS_DEVICE_IP

我就scp到了设备上，手动执行了dpkg的命令，然后respring竟然没效果，只好reboot了一下，看到了刚刚的app已经被安装上了！！！
