---
layout: post
title: 更新Mac下的ruby
comments: true
date: 2012-02-05 00:00
categories: mac ruby
---

刚刚说了要开始学ruby了，但发现Mac下的ruby版本挺低的，才1.8.7，现在官方的都1.9.3了，于是更新，发现这个更新不大容易，到底现在该不该爱Mac呢？！

修改一下/usr/local的权限：(如果不修改的话，或许会出现通过brew安装的软件无法自动创建符号链接到/usr/local/bin中的情况，如果不能自动创建链接过去的话，麻烦是一个方面，关键是后面做的一些工作基本都白费了，可能你运行的一个软件是在/usr/bin中存在的，那样就不会自动搜索到你用brew安装的那个了。详情找找brew的工作原理吧：)


{% codeblock lang:bash %}
sudo chown -R `whoami` /usr/local
{% endcodeblock %}

首先我用了大家推荐的Homwbrew管理工具，这里安装完homebrew后需要在自己的bash配置文件中加入新的path：


{% codeblock lang:bash %}
export PATH=/usr/local/bin:$PATH
{% endcodeblock %}

把这行加入到bash_profile中吧，这样就能让homebrew发挥作用了，你首先就能用上更新了的程序而不是从默认路径查找。（如果以前用了MacPorts的话你也会和我一样看到MacPorts的export命令，要去掉他们，或者你把Homebrew的export命令写在下面，这样能覆盖掉，既然我已经删除了MacPorts，所以干脆删除掉！）

关闭terminal，重新加载刚才的bash_profile，这样就能用Homebrew了。

首先安装git，自己和Homwbrew都用得到：


{% codeblock lang:bash %}
brew install git
{% endcodeblock %}

接着更新一下Homebrew的源：


{% codeblock lang:bash %}
brew update
{% endcodeblock %}

然后安装了ruby后就能用gem来更新系统了：

安装ruby：

{% codeblock lang:bash %}
brew install ruby
{% endcodeblock %}

更新系统：


{% codeblock lang:bash %}
gem update --system
{% endcodeblock %}

后面的安装rails等操作就可以用gem来做了，看看自己的ruby版本，已经是1.9.3p0(2011-10-30)