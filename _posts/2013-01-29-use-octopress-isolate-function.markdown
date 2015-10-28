---
layout: post
title: "use octopress isolate function"
date: 2013-01-29 08:27
comments: true
categories: blog
---

以前搜到过octpress的isolate功能，今天终于用上了，真TMD好用（除了操作稍微麻烦一点）

使用isolate的注意：filename是除了日期外的名字，有空格得用短杠隔开，比如我的这篇就得用`rake isolate[use-octopress-isolate-function]`才可以。还有啊，我希望isolate这个功能自动点不知道靠不靠谱，就是new_post就顺带着执行isolate，如果你一般不修改以前的post那还是可行的，实在修改的话只好integrate过来再isolate需要修改的那篇修改喽。

这样的话generate的速度会很快。
