---
layout: post
title: "在MacOS上配置dnsmasq"
date: 2013-01-22 22:26
comments: true
categories: dev 
---

最近那个伟大的墙把我们敬爱的git大神封锁了，无奈很多代码都托管在上面，其中也不乏很多商业项目。自己的几个blog也都放在上面，倒不是因为在那里免费，而是这已然已经成为程序员们的一种生活style。

ubuntu下有个dnsmasq可以连接别的dns，这样能够避免dns污染导致上不了github的问题。相关配置不算难，下面记录一下在MacOS下的dnsmasq配置方法。

1.使用brew安装dnsmasq

brew install dnsmasq

2.修改一下dnsmasq的配置文件名字

cp /usr/local/opt/dnsmasq/dnsmasq.conf.example /usr/local/etc/dnsmasq.conf

3.加入MacOS的启动项中

sudo cp -fv /usr/local/opt/dnsmasq/*.plist /Library/LaunchDaemons

4.加载并启动dnsmasq，如果没有出现什么错误就开始配置dnsmasq

sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist

5.配置dnsmasq，把no-resolve的注释去掉，加入`server=xxx.xxx.xxx.xxx#nnnn`

mate /usr/local/etc/dnsmasq.conf

server的值可以从dns.v2ex.com中找到，“#”后面的是端口号，比如v2ex那个用3389

6.重启dnsmasq

sudo launchctl stop homebrew.mxcl.dnsmasq

其实无需再执行`sudo launchctl start homebrew.mxcl.dnsmasq`这句了，因为你load了plist进去就已经启动了，如果此时stop的话会再自动start，所以没必要再start。要想关闭请使用unload（就修改上面的4即可）

7.把网络的dns设置成127.0.0.1，这样你才能用自己的dns服务

至此，我们的git大神就回归了。
