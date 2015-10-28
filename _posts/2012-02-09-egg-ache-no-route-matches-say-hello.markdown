---
layout: post
title: 蛋疼的No route matches “/say/hello”
comments: true
date: 2012-02-09 23:01
categories: study ror
---

现在有些后悔买的那本书了，《web开发敏捷之道第三版》，那本书的代码使用的是rails2.2.2，真够2的，现在用的是3.2.1，作者说有不少代码已经更改了，但没想到会差得连我都能看出来，我只是个初学者啊！好在我还能稍稍应付自如，后面可能就会更加累了！

一开始在helloworld部分就遇到一个问题，用rails generate controller say后根本不能自动添加一条routes，找了原作者的wiki更新发现这里已经需要自己修改routes的内容了，不过也好，消去一行注释即可：）

感谢[这里](http://www.xiaoyangsheng.com/2011/02/routing-error-no-route-matches-sayhello/)

如果还有谁遇到类似不兼容问题，请看[作者的wiki更新](http://pragprog.com/wikis/wiki/ChangesToRails)吧，希望有帮助！