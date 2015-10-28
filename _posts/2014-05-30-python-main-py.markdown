---
layout: post
title: "python-main-py"
date: 2014-05-30 21:05:20 +0800
comments: true
categories: dev
---

python的`__main__.py`文件，通常，一个package下有一个`__init__.py`文件标识这是package，同样可以有一个`__main__.py`文件，有了后你就可以这样运行一个脚本：`python script_dir`或者把这个dir打包成zip，可以使用`python zipball.zip`来执行，python会执行`__main__.py`中的语句。