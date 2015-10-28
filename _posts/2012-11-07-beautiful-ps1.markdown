---
layout: post
title: "beautiful PS1"
date: 2012-11-07 21:12
comments: true
categories: shell
---

今天又加了不少红绿颜色的字在各种输出上，看起来更加顺眼了，无奈server的网关被人修改了，我们也不敢轻易改动，因为编辑们正在使用，怕改了他们不能访问了。。。那个负责人到我们下班都没回来，真不知道干嘛去了。

研究了一下这种颜色是怎么回事，原来是在一个字符串前后加上颜色标记，就和html的标记一样，只不过颜色标记更加让人难以理解。临下班我想研究一下如何做一个autocomplete的veil出来，可惜都搜不到什么资料，可能这不是什么很值得人们写的东西吧，竟是些讲按Tab可以complete，但不说你怎么写code可以实现这种，猜想是有什么hook可以监听tab事件吧：）后来在[这里](http://hi.baidu.com/widebright/item/5f92a4cf65c79709c710b2ac)找到一篇文章，介绍了一点原理和写法，准备翻翻我那本《Shell脚本学习指南》看看有没有帮助。

研究这个的副产品就是看到了PS1的介绍，可以搭配出漂亮而功能强大的PS1。

其实PS1就是一个字符串，Ta规定了提示符的那一行会怎么显示出来以及显示什么，这里面你可以写一些函数调用、配色什么的，terminal会自动帮你调用，然后就是显示出来。给你看个展示效果：

![PS1 pic](http://pic.yupoo.com/dawncold0/CoN0yCPa/medish.jpg)

是不是很好看呢？再看看让Ta显示成这个样的PS1字符串长什么样吧：

{% codeblock lang:bash %}
export PS1='\[$(tput bold)\]\[$(tput setaf 3)\]\u\[$(tput setaf 2)\] [\t] \[$(tput setaf 1)\]\W=>\\$\[$(tput sgr0)\] '
{% endcodeblock %}

相关颜色可不是那么好记忆的如果你用\033、\032这样标记的话，推荐个网站，你可以直接设置好效果，然后复制过来就可以了：[http://www.kirsle.net/wizards/ps1.html](http://www.kirsle.net/wizards/ps1.html)
