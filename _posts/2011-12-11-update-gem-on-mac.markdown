---
layout: post
title: 更新mac下的gem
comments: true
date: 2011-12-11 19:49
categories: mac
---

要不是弄github的pages我也不会接触到gem。

lion的gem是1.3.6这个超低版本，现在最新是1.8.12，我下载了update_rubygem1.8.12.gem，用gem安装上了：

{% codeblock %}
sudo gem install update_rubygem-1.8.12.gem
{% endcodeblock %}

然后不知道怎么用了，于是用gem开启来一个server玩：

{% codeblock %}
gem server
{% endcodeblock %}

不小心看到已经安装了两个gem，执行命令分别是gem和update_rubygem，于是我执行了后面那个，就更新到了1.8.12

