---
layout: post
title: WTForms中的FileField验证
comments: true
date: 2012-07-05 20:17
categories: python
---

本来打算针对上传的图片进行验证，不过发现在form中加入enctype属性之后原本针对FileField的验证就不管用了，field.data始终是None，但是去掉enctype属性就ok，不过去掉之后不能上传文件了，所以最终只好去掉验证，在request中进行验证。

比如我是这样验证没有选择图片的：


{% codeblock %}
form = xxxForm(request.form)
f = request.files["image"]
if len(f.filename) == 0:
 form.image.errors = ValidationError(u"need a pic file!!!")
 return render_template("xxx", form = form)
......
{% endcodeblock %}

如果有不同的见解请告诉我哦！