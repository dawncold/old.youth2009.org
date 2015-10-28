---
layout: post
title: 生产环境下的flask调试
comments: true
date: 2012-07-17 09:36
categories: python
---
生产环境是：nginx+uwsgi+flask+sqlalchemy等等等

自带的调试功能比较好用，也能很方便的查看各种变量的值，不过在生产环境中调试并不是那么容易。需要在uwsgi开启的时候传入“--catch exceptions”：

{% codeblock lang:bash %}
uwsgi -s :9090 -M -p 4 -t 30 --limit-as 128 -R 10000 -d uwsgi.log --vhost --catch-exceptions
{% endcodeblock %}

在flask的app中要设置config中的PROPAGATE_EXCEPTIONS = True才可以在遇到错误的时候直接输出到页面上。

昨晚部署到服务器中，发现好多地方是500号错误，根本不知道在哪里出的错误，今天打开了这些才发现是jinja2模板中的do方法不识别，原来我把这个加载do操作放在了比较靠后的地方，在生产环境下不会去调用app了，所以原本写在`if __name__ == "__main__"`里面的东西就不会再调用了：）