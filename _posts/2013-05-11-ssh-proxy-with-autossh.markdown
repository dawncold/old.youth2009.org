---
layout: post
title: "ssh-proxy-with-autossh-in-mac"
date: 2013-05-11 13:10
comments: true
categories: gfw
---

在Mac下原来一直用iSSH，好处是简单，功能够用，但有个缺点很致命，ssh有时候会断开，谁知道最终是什么原因导致的，但iSSH不会自动重连，只是提示你。在忍受了很久之后换成了autossh，它没有GUI，但可以在ssh断开后自动重连。

1.使用brew安装autossh，或者用其他工具安装autossh，包括手。

`brew install autossh`

2.配置你的海外主机，保证你可以不用密码登陆。无非就是在authorized_keys中加入你的public key。自己用ssh登陆只要不用密码了就ok。

3.用autossh连接。

`autossh -M 20000 -f -p REMOTEPORT -D LOCALPORT xxx@8.8.8.8 -N`

autossh就3个参数，-M、-f、-V，其中-V是显示版本，其余两个参数的意思看[文档描述](http://www.harding.motd.ca/autossh/README "autossh README")吧。

如果你没改远程主机ssh的默认端口，那就省略-p REMOTEPORT。

指定一个LOCALPORT，一般用什么1080，我用9998。

后面是ssh连接信息，最后-N表示port forward不用terminal交互。

4.(可选操作)如果你比较懒，希望login系统的时候自动帮你连接上ssh，Mac下使用launchd来做，推荐使用Lingon这个app，是个launchd的GUI。

添加一个My Agents就可以了，何时运行那里我勾选了at startup or login，生成的plist会放在~/Library/LaunchAgents/中，生成的内容如下：

{% codeblock %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>Label</key>
<string>autossh</string>
<key>ProgramArguments</key>
<array>
<string>/usr/local/bin/autossh</string>
<string>-M</string>
<string>20000</string>
<string>-f</string>
<string>-p</string>
<string>9999</string>
<string>-D</string>
<string>9998</string>
<string>google@8.8.8.8</string>
<string>-N</string>
</array>
<key>RunAtLoad</key>
<true/>
</dict>
</plist>
{% endcodeblock %}

至此，开机自动连接ssh，自由surfing吧。
