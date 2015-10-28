---
layout: post
title: "crontab a python script"
date: 2013-07-21 22:28
comments: true
categories: python
---

今天用python写了个[小程序](https://github.com/dawncold/stuff/blob/master/ping_test.py)检测网络是否通断，如果断了就弹出一个Notification，当然是Mac上的，并且弹出一个terminal，带着执行ping www.baidu.com。

一开始用Lingon加入到启动项中并且打算2分钟执行一次，几经折腾终于失败，弃之。打算用crontab弄。

好歹算是可用了吧，注意的是：script的开头写/usr/bin/python，crontab中写PATH没用，得写PYTHONPATH才管用，而且我还写了MAILTO（现在不知道管什么用）。由于在script中用了popen，可能这个需要依赖一些环境或者是tty（这是从stackoverflow上看来的，具体可以搜popen crontab），现在想来launchd是不是也因为如此没能成功启动呢？（总提示255退出代码）

crontab:

{% codeblock lang:bash %}
MAILTO="dawncold@me.com"
PATH=/Users/dawncold/.rvm/gems/ruby-1.9.3-p286/bin:/Users/dawncold/.rvm/gems/ruby-1.9.3-p286@global/bin:/Users/dawncold/.rvm/rubies/ruby-1.9.3-p286/bin:/Users/dawncold/.rvm/bin:/Library/Frameworks/Python.framework/Versions/2.7/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/opt/X11/bin:/usr/local/MacGPG2/bin
PYTHONPATH=/usr/bin
* * * * * /Users/dawncold/ping_test.py > /Users/dawncold/pt
{% endcodeblock %}
