---
layout: post
title: git的导出功能
comments: true
date: 2011-07-10 08:13
categories: git
---

用git管理项目的优势大家可能都看了许久了，我也是因为如此才用了git而不是svn、cvs这些。其实我是挺喜欢喜新厌旧的，因为新东西的出现并流行一定是比原来的有所突破，并且大多数人喜欢这种变革，所以为何不喜欢呢？

用git管理项目不可避免要遇到导出功能，在svn和cvs上应该叫export功能，git上的这个功能似乎没找到，要这样做：先打包，再解压到一个地方去。还能接受吧。

{% codeblock %}
git-archive --prefix=map/ master | tar -x -C ../map_e/
{% endcodeblock %}

稍微解释一下，prefix指明了用哪个仓库，后面的master应该就是branch的名称了，然后把这些传递给了tar，因为不指明--format的时候默认用了tar方式打包，所以这里传递给tar解压到上层目录的map_e中，当然实际工作可以解压到生产服务器上去。