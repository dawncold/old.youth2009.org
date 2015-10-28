---
layout: post
title: Git使用重新学习（标签）
comments: true
date: 2012-01-26 17:29
categories: study git
---

打标签，挺有用的一个功能，一般是加版本号吧。v1.0，v2.0，vN.0

git tag是看标签

git tag -a 是加带附注的标签，（还有轻量级标签不用加-a，直接给出标签名字完事），接下来一个参数是标签名字，再者需要-m引出附注内容，完整就像这样：git tag -a v1.0 -m 'first version'

加完后可以show一下：git show v1.0，所谓附注就是包含了很多提交者的信息，以后可以慢慢查证使用。

如果你有GPG的话还可以签署标签，把前面的-a改成-s即可，-s是signed的意思，-a是annotated的意思。（刚刚尝试了一下-s，可惜Mac系统上没装gpg软件，签署失败，但大多linux系统都会有的吧，Mac系统的用户请从[这里](http://www.gpgtools.org)下载GPGTools）

刚才用GPG签名了，现在验证一下：git tag -v xxx，-v就是verify的意思，比如我得到了如下的提示信息：

{% codeblock lang:bash %}
object a20e6b9c2433e88a9da63abd8d74ddede9bccde6
type commit
tag v_2012-01-26-s
tagger dawncold <loooseleaves@gmail.com> 1327569076 +0800

signed this tag
gpg: 于 四  1/26 17:11:24 2012 CST 创建的签名，使用 RSA，钥匙号 1B1ECF39
gpg: 完好的签名，来自于“dawncold <loooseleaves@gmail.com>”
{% endcodeblock %}

很可惜，默认tag是不被push到远程仓库中的，如果要分享你的tags，在push的时候要显示地写明：git push origin [tag-name]，推送所有tags可以直接用--tags来代替tag-name参数

删除tag需要用-d完成：git tag -d [tag-name]