---
layout: post
title: 动态验证表单也不难
comments: true
date: 2011-02-05 23:06
categories: js
---

一般来说现在的注册、登录的表单验证都是在浏览器这一级先做一个合法性验证，这样能够缓解服务器的压力，否则这些合法性验证都要移到服务器上，无论从性能和表现力都不及在浏览器用一些很炫的效果来验证。我使用了jQuery这个javascript库完成了表单的动态验证，核心不算难。一开始我都是参考豆瓣的注册页面，他们现在用的也是jQuery来做这块，代码看起来超长，还分了好几个js文件来组织，不是他们的前端工程师谁也看不懂（我真怀疑他们的前端工程师是不是能看懂）。 我做得很简单，不过看起来也能用： 一般有个空的div显示提醒文字，假设input的id是xxx，我们这样

{% codeblock lang:js %}
$("input#xxx).focus(function(){$("suggestion").html(插入提示文字);});
{% endcodeblock %}

就能够在焦点进入input的时候提示一些文字了，然后在  


{% codeblock lang:js %}
focusout(function(){xxxxxx});
{% endcodeblock %}

中先remove插入的文字，再添加新的文字。 一般在focusout中进行一次查询，然后进行更改文字，是能够注册还是已经被占用，在查询的时候我使用的是$.getJSON函数，用GET方式提交查询看起来比较帅，当然最好做简单的提交，因为用了getJSON的方式，返回值一定是要json，我的服务器端脚本使用的是php，看到jQuery官方例子中提及了json_encode函数，接收array，正好能够返回我的查询结果，SQL查询返回结果用fetch_assoc放进一个array了。getJSON第三个参数是个callback函数，是结果成功返回时调用的函数，更改相应提示文字就在这里面进行，这个callback有个参数data，应该就是包含json的数据吧，用点运算符取到响应结果进行操作。