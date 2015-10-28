---
layout: post
title: "NotImplemented-in-python"
date: 2014-12-26 21:03:20 +0800
comments: true
categories: study
---

It's best to return `NotImplemented` in magic method(e.g. `__eq__`, `__ne__`, etc), see [here](http://shahriar.svbtle.com/python-notimplemented-type) for details.

{% codeblock lang:python %}
# example.py

class A(object):
    def __init__(self, value):
        self.value = value

    def __eq__(self, other):
        if isinstance(other, A):
            print('Comparing an A with an A')
            return other.value == self.value
        if isinstance(other, B):
            print('Comparing an A with a B')
            return other.value == self.value
        print('Could not compare A with the other class')
        return NotImplemented

class B(object):
    def __init__(self, value):
        self.value = value

    def __eq__(self, other):
        if isinstance(other, B):
            print('Comparing a B with another B')
            return other.value == self.value
        print('Could not compare B with the other class')
        return NotImplemented
{% endcodeblock %}

`a` is instance of ClassA, and `b` is instance of ClassB, if we invoke `a == b`, we will get the result, True or False, but if we invoke `b == a`, we will also get the result! Because of we return `NotImplemented` in Class B's `__eq__` method, runtime could invoke Class A's `__eq__`, that method can compare A and B.