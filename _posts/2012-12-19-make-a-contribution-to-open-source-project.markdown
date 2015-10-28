---
layout: post
title: "给开源项目做贡献了"
date: 2012-12-19 21:18
comments: true
categories: dev
---

惭愧，第一次给开源项目做贡献竟然是现在，其实早就想帮着做点啥了，无奈技术能力不足，终于发现一个机会，给progit的README文档添加MacOS用户的使用方式，可惜噩梦也是这样开始的。

一开始添加了usage for macos users，commit然后push，作者和我说少一个blank line，我加了再commit和push，另一个开发者和我说你不应该多次commit，需要说清楚commit的工作而不是一味用commit修改，我改好了发现remote的版本和本地不一样，因为我是在上一个版本的基础上amend后再提交的，无奈之下我merge了remote然后commit又push，这时候作者跳出来一对一教我怎么做了，有不少细节地方需要注意，比如完全的command line可以在markdown中用tab的indent，而list的indent和tab是完全不一样的。。。又给我罗列了markdown的语法。我让他写一个正确的给我看一下，他真的就给我写了一遍，但是他给希望让别人来做这部分工作而不是自己来做，并不是自己能力不足什么的，光是在我这里付出的时间就远超编辑好几个版本的README了。这点在国内开发者的身上很难发现吧？！

最后当然是pull request被接受了：）这次经历很难得！
