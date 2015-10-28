---
layout: post
title: python的继承
comments: true
date: 2011-06-05 18:41
categories: python
---

python继承过来的子类在初始化的时候不会自动调用父类的构造函数，得自己手动调用。 这里给一点简单的示例代码:


{% codeblock %}
#! /usr/bin/python
# -*- coding:utf-8 -*-
# Filename : inherit.py

class Person:
   def __init__(self,name,age):
       self.name = name
       self.age = age
       print "init for %s" % self.name

   def tell(self):
       print "name:%s age:%d" % (self.name,self.age)

class Teacher(Person):
   def __init__(self,name,age,salary):
       Person.__init__(self,name,age)
       self.salary = salary
       print "init for teacher %s" % self.name

   def tell(self):
       Person.tell(self)
       print "salary:%d" % self.salary

p = Person('tianzhen',20)
p.tell()

tea_p = Teacher('zhenzhen',20,1010000000)
tea_p.tell()
{% endcodeblock %}
