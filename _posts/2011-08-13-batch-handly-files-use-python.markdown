---
layout: post
title: python批量处理文件
comments: true
date: 2011-08-13 15:30
categories: python
---

从某网站上下载了几个压缩包，里面全是目录，每个目录下都有一个doc文件，但可恶的是这些doc文件被换了扩展名，原本是xxx.doc现在变成xxx.doc.resx，我得用python批量处理一下：


{% codeblock %}
#! /usr/bin/python
# -*- coding:utf-8 -*-
# 遍历所有目录，把resx文件扩展名删掉

import os

current_path = os.getcwd()
allsubdir = os.listdir(current_path)

for subdir in allsubdir:
   subdir_path = './' + subdir
   if os.path.isdir(subdir_path):
       files = os.listdir(subdir_path)
       for _file in files:
           basename = os.path.basename(_file)
           allname = os.path.splitext(basename)
           if '.resx' in allname:
               print 'resx file %s' % basename
               without_resx = allname[0]
               os.rename(subdir_path+'/'+_file,without_resx)
           else:
               print 'not resx file'
               continue
{% endcodeblock %}

还用了一个删除空目录的脚本：


{% codeblock %}
#! /usr/bin/python
# -*- coding:utf-8 -*-
#删除空目录

import os

alldir = os.listdir(os.getcwd())
for _dir in alldir:
   if os.path.isdir('./'+_dir):
       print 'dir: %s' % _dir
       if os.listdir('./'+_dir):
           print 'have something %s' % os.listdir('./'+_dir)
       else:
           os.rmdir('./'+_dir)
   else:
       print 'file or others'
{% endcodeblock %}

用python，很快乐！

