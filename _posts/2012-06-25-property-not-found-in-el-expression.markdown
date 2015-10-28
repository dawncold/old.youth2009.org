---
layout: post
title: 关于EL表达式中的Property 'name' not found on type java.lang.String错误
comments: true
date: 2012-06-25 09:00
categories: S2SH
---

好了，我直接说自己遇到的情况，就是上面这行提示，找不到name属性，在java.lang.String中，仔细看哦，这句话的意思是你在一个String类型中找name属性，当然不会找到了！！！因为本来String中就没有name属性。

初衷是一个list中，里面的每个元素都有name属性，但是经过JPQL查询后的list给了jsp页面，在输出的时候就得到了这样的提示。实际上我是JPQL写错了，我直接得到了具体的值，所以是String类型的一个list，应该用JPQL得到实体，这样就OK了。

比如：得到的是Student实体，可以用里面的name属性。


{% codeblock lang:bash %}
SELECT s FROM Student s, School sc WHERE sc.city = '北京' AND s.school.id = sc.id AND s.name LIKE '张%'
{% endcodeblock %}

但是：得到的就是具体的name了，再用name属性就会出现上面的错误


{% codeblock lang:bash %}
SELECT s.name FROM Student s, School sc WHERE sc.city = '北京' AND s.school.id = sc.id AND s.name LIKE '张%'
{% endcodeblock %}

这种错误很难搞的！！！