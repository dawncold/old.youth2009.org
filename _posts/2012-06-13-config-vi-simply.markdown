---
layout: post
title: 简单配置一下vi
comments: true
date: 2012-06-13 22:26
categories: vi
---

看到vpsee上的vi打开网页啥的都能自动高亮，原本一直用着纯文本方式vi的我动心了，搜索了一点点配置，加入这些配置到~/vimrc这样的文件中后，打开vi就能自动加载配置。

下面的分别是：显示行号、自动缩进、开启语法高亮、编辑背景为暗色调、开启粘贴（传说复制过来的代码不会乱掉）


{% codeblock lang:bash %}
set number
set autoindent
syntax enable
set background=dark
set paste
{% endcodeblock %}

vim是和emace同样重量级的编辑器，如果你是一个Linux控你肯定明白那句话，vi是vim的前身（允许我这样描述吧），所以配置都是这些编辑器的看家本领，这几条简单配置仅仅是个入门，还可以根据自己的需要添加修改