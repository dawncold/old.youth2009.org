---
layout: post
title: "useful-shell-command"
date: 2013-12-07 22:28:53 +0800
comments: true
categories: shell dev
---

找到size为0的文件，并删除：`find -type f -size 0 | xargs rm`

替换Linux的换行成windows的：`ls | xargs perl -i -pe 's/\n/\r\n/g'`

批量改名哦（把*.md改为*.markdown）：

{% codeblock lang:bash %}
for i in `ls *.md`;do mv $i `echo $i | sed 's/.md/.markdown/'`;done
{% endcodeblock %}
