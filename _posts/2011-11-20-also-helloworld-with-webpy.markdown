---
layout: post
title: 又是helloworld
comments: true
date: 2011-11-20 23:58
categories: python
---

学计算机编程语言的人都有helloworld情节，不管学成什么样，他们写helloworld的能力都很强。


{% codeblock %}
import web

urls = ("/hello", "hello")
app = web.application(urls, globals())

class hello:
   def GET(self):
       return "hello, world"

if __name__ == "__main__":
   app.run()
{% endcodeblock %}

今晚已经开始了Web.py的学习阶段。

看官方介绍的在Mac系统下安装webpy有点特别，于是我直接使用了easy_install的安装方法，不知道自己以前安装过easy_install这个软件管理工具，直接使用就好了，不过最好加上sudo，否则会提示无法创建什么目录，权限不够吧。

安装完web.py后就能使用框架来写东西了，上面的helloworld就算是。

通过这个简单的helloworld能够学到一点框架的知识——在urls中一个url字符串对应一个处理的类对象，如果需要为这个app配置多个url和对应的处理类，就需要使用add_mapping方法，这些内容请参考[官方的api](http://webpy.org/docs/0.3/api#web.application)，很是简单，具体不在此赘述。

第一天就学到这里，以后就要变学习变开发了。