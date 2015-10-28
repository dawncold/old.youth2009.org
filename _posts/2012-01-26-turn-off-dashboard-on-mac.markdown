---
layout: post
title: Mac系统关闭dashboard
comments: true
date: 2012-01-26 00:49
categories: mac
---

一开始感觉dashboard这个东西挺好的，加上了好几个小插件玩，但现在发现使用频率超低，所以干脆想办法关闭吧，听说还能节约部分内存和提升开机速度，对这些倒是不太关心，只能有种不用就关闭的态度驱使着我。

关闭命令：

{% codeblock lang:bash %}
defaults write com.apple.dashboard mcx-disabled -boolean YES;killall dock
{% endcodeblock %}

如果需要重新开启，请使用这条命令，包括了killall Dock：

{% codeblock lang:bash %}
defaults write com.apple.dashboard mcx-disabled -boolean NO;killall Dock
{% endcodeblock %}
