---
layout: post
title: nginx下的location配置
comments: true
date: 2011-07-10 20:15
categories: nginx
---

原来的location只是处理了“/”的情况，结果访问一个目录，即使此目录下有index.html也不会成功显示，于是改成了这样：

{% codeblock %}
location ~.*\.(php|php5)?$
{
    处理php
}
{% endcodeblock %}

这样之后，发现直接访问目录或者域名的时候不能正常显示了，必须跟上index.php这样的才可以。

最终改成这样，解决了问题：


{% codeblock %}
location / {
               root html;
               index index.html index.php;
}
location ~.*\.(php|php5)?$ {
处理php
}
{% endcodeblock %}
