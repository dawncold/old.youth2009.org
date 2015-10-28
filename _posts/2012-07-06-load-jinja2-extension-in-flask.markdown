---
layout: post
title: Flask中Jinja2加载扩展
comments: true
date: 2012-07-06 20:34
categories: python
---

代码中我把jinja2的语法改成了这样的，{##}，因为这样就不会和blog生成html冲突了，大家改回来就可以。

在Flask中接触到了jinja2，由于某个简单的需要——在模板系统中计算某些订单项的总价格，必须打开Jinja2的“do”扩展，用一种hack的方法来计算，十分不喜欢这样，但能用。

在Flask的API中没有公开这样的方法，不过在邮件列表的索引里找到了：

{% codeblock %}
app.jinja_env.add_extension("jinja2.ext.do")
{% endcodeblock %}

还想多说一下Jinja2的set方法，超级不爽的一个方法，原本以为set出来的变量就可以和python中的变量一样使用呢，结果在这里的set出来的变量也就是一个助记作用，根本不能保存新的值，也就是说这里的变量相当于我们通常意义上的常量！！！

{% codeblock lang:html %}
......
{# set total_price = 0 #}
{# for item in order.items #}
{# total_price = item.meal.price * item.quantity #}
<p class = "order_list_item">{{ item.meal.name }}

{# endfor #}
</td>
<td>{{ total_price }}</td> 
......
{% endcodeblock %}

原本希望在for外面设置一个变量，然后在for中计算好total_price使用，结果根本不行，这样写的结果就是“找不到total_price变量”，如果去掉for中对total_price的引用就可以正常看到total_price，是0。总之，这里set出来的变量就是一个常量了！！！后来打开了do扩展，把total_price设置成一个list，然后在for中把没一项的价格都append进去，最终输出的地方用了jinja2的filter计算总和。大约会写成这样：

{% codeblock lang:html %}
......
{# set prices = [] #}
{# for item in order.items #}
{# do prices.append(item.meal.price * item.quantity) #}
<p class = "order_list_item">{{ item.meal.name }}

{# endfor #}
</td>
<td>{{ prices|sum }}</td> 
......
{% endcodeblock %}

相信jinja2改进set之后会是一个很不错的模板系统：）
