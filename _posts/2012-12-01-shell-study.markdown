---
layout: post
title: "shell study"
date: 2012-12-01 11:52
comments: true
categories: study shell
---

sed是个极其强大的东西，今天开始学习一点点：）

以前的一个sed的命令终于明白了：

{% codeblock lang:bash %}
find ./ -name '*.html' | xargs sed -i 's/iso-8859-1/utf-8/g'
{% endcodeblock %}

这是替换html编码用的一个语句，find出当前目录下的html文件名字，然后传给sed，当然这里用到了xrags中转，其实没有的话也ok（除非你不用-i模式），sed用了-i模式，可以编辑文件内容保存，并且存一个备份，当然你得传入一个扩展名字才能保存，没有的话就不存和没有-i效果一样。后面的一个字符串，s表示用正则匹配，s后面的是一个分隔符，可以用斜杠，可以换你喜欢的，但后面都要统一起来，上面的意思是iso-8859-1这个替换成utf-8，最后的加的/g是表示global替换，全部替换，否则就替换一次。

后来看起别的书来了。