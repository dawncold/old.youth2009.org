---
layout: post
title: "do something using refactor"
date: 2013-02-03 11:22
comments: true
categories: work@honovation dev
---

最近在做发送短信的时候犯了个错误——修改配置文件没有使用重构方式。dev环境和pro环境中有相同名字的配置，只是值不一样，再修改了dev中的配置name做开发，但pro环境中的name还是原来的，导致上线后拿不到配置，发不出短信去。。。

以后为了防止遗忘，还是用重构吧！！！
