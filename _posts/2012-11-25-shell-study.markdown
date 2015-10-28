---
layout: post
title: "shell study"
date: 2012-11-25 10:24
comments: true
categories: shell study
---

上次说到了echo有可能出现标准不一致的情况，所以建议使用printf，但如果你只是使用最简单的echo输出一段话，那还是没问题的。printf更加复杂，功能和C语言中的printf基本相同。

IO重定向默认在你登录的时候就把standard input/output绑定到了terminal中，所以你可以在terminal中完成很多工作。

简单的重定向：“>”、“<”、“>>”，分别是改变重定向input、output，最后一个是附加到某个文件，如果你在使用">"的时候不存在目标文件，那么会被创建出来，如果已经存在就会被覆盖掉，原有数据丢失，如果使用">>"则会追加到目标文件中，原有数据依然存在。

管道也是重定向的一部分，prog1 | prog2，可以把prog1的标准输出重定向到prog2的标准输入上，如果你需要连接多个程序的时候，最好用管道方式，这样比临时文件效率高很多（据说10倍）。在使用管道的时候应该逐级让数据量减少，这样能够提高脚本的整体性能，例如在sort之前，你可以grep出需要sort的行，这样会好一些：）

特殊文件：/dev/null 和 /dev/tty。null这个被称为bit bucket，传输到这里的东西都会被丢弃，就如同黑洞一般：）程序把文件写入到这里就会被认为是成功的，但实际什么都没做，例如：

{% codeblock lang:bash %}
if grep pattern myfile > /dev/null
then
…
else
…
fi
{% endcodeblock %}
可以做一个探测，是否myfile有pattern，这样不会产生输出。

/dev/tty的功能是，当程序打开这个文件时会重定向到一个terminal，在需要输入密码的时候用的到：

{% codeblock lang:bash %}
printf "Enter password: "
stty -echo #关闭自动回显输入的字符功能
read pass < /dev/tty
printf "Enter Again: "
read pass2 < /dev/tty
stty echo #打开自动回显输入的字符功能
{% endcodeblock %}

shell的PATH中最好不要放入当前目录这一选项，这会带来安全问题，所以干脆就不要这么想了：）
