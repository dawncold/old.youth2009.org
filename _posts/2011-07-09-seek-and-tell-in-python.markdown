---
layout: post
title: 简要写写python的file中的tell和seek
comments: true
date: 2011-07-09 15:12
categories: python
---

对于一个file，调用tell()能够知道现在的文件位置。seek()是改变文件位置。  比如文件中有3行句子，readline后位置就到了第一行的最后，再readline就到了第二行的最后，readline后我调用了tell，看到的结果就是这样的。输出完tell()我又使用了seek(0),这样文件位置就回到开头了，下次再调用readline就会输出原来第一行的内容了，这应该是很容易理解的。不明白可以亲自试试。

{% codeblock %}
from sys import argv

script, input_file = argv

def print_all(f):
   print f.read()

def rewind(f):
   f.seek(0)

def print_a_line(line_count, f):
   print line_count, f.readline()

current_file = open(input_file)

print "First let's print the while file:\n"
print_all(current_file)

print "Now let's rewind, kind of like a tape."
rewind(current_file)

print "Let's print three lines:"

current_line = 1
print_a_line(current_line, current_file)
print "current_pos:%d" % current_file.tell()
rewind(current_file)

current_line += 1
print_a_line(current_line, current_file)
print "current_pos:%d" % current_file.tell()

current_line += 1
print_a_line(current_line, current_file)
print "current_pos:%d" % current_file.tell()
{% endcodeblock %}
