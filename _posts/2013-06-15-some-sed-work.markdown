---
layout: post
title: "some-sed-work"
date: 2013-06-15 16:34
comments: true
categories: study shell
---

博客内容是从wordpress转过来的，不可避免有很多地方没转换好，当时懒得弄，今天得空学习Shell编程，讲到了sed，就又搞了一下，基本满意了。

以前用sed替换过分类等简单的文字错误，今天主要是把一些html给替换掉了。

把`<p>`删掉，在删掉`</p>以及<br />`后面加换行等：

`sed -i "" -e 's;</p>;\'$'\n;g' *.markdown`

`sed -i "" -e 's;<br />;\'$'\n;g' *.markdown`

需要注意的是Mac OS中的sed和我看到的很不一样，所以这个替换都是特殊的，来自[这里](http://cafenate.wordpress.com/2010/12/05/newlines-in-sed-on-mac/)