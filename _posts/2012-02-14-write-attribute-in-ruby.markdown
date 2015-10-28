---
layout: post
title: Ruby中的write_attribute
comments: true
date: 2012-02-14 16:06
categories: study ruby
---

有时候想修改一下自己的setter方法，于是会容易犯这样的一个错误：

{% codeblock lang:ruby %}
def password=(pwd)
   @password = pwd
   return if @password.blank?
   create_new_salt
   self.password = xxx
 end
{% endcodeblock %}

最后那行使用了self.password= xxx，你有没有注意到我们这个方法就是password=，你在自己调用自己，如果有条件停止的话，那这叫递归，如果没有的话，这就是死循环喽，ruby可能会抛出一个stack too deep的错误（rails至少会这样说），此时需要一个magic！


{% codeblock lang:ruby %}
write_attribute(:password, User.encrypted_password(self.password, self.salt))
{% endcodeblock %}

使用write_attribute(xxx,jjj)即可，意思就是把jjj赋值给xxx了，因为此时正好在定义xxx，所以不能用xxx = 这样的方法赋值。