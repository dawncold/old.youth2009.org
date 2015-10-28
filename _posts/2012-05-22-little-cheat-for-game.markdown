---
layout: post
title: 小作弊玩游戏
comments: true
date: 2012-05-22 23:31
categories: mac
---

有这么一个小游戏，按照顺序输入字母表的26个英文字母，看看你输入的总时间是多少。有个变态的人竟然在2s内就输入了26个字母，而且不允许有任何错误，真心佩服！！！

我试了试，快的话我只能在6s左右完成，根本上不了排行榜，于是我考虑作弊……


{% codeblock lang:bash %}
tell application "Google Chrome"
activate
repeat with i from 0 to 25
delay 0.04
tell application "System Events"
keystroke (ASCII character of (97 + i))
end tell
end repeat
end tell
{% endcodeblock %}

不减速的话系统根本无法记录，所以还是减速了，这个速度正好拿到第一名的位置，OK，剩下的让人去羡慕吧！！！

感谢Apple提供的AppleScript这样优秀的脚本工具～

