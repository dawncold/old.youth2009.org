---
layout: post
title: 为项目搭建git版本控制
comments: true
date: 2011-02-24 17:37
categories: git wodeyitian
---

这两天一直跟随网上的各路人马学习git的使用，也就是刚刚到了能够用一点git的命令而已的地步，这个东西还是得到了具体的项目中才能慢慢熟悉了解。本来打算好好学习svn，现在看来就不必了，学习一个更加有生命力的吧！ 在我的vps上搭建了git服务器环境，下面就记录一下过程： １.安装git就不再多说了，我似乎把redhat中的一个仓库加入了rpm，直接yum install -y git安装了，不如下载源代码安装的git版本高，我这里似乎只有１.５的版本。 ２.我使用了gitosis来管理所有的项目，所以：  


{% codeblock %}
yum install python-setuptools
git clone git://eagain.net/gitosis.git
cd gitosis
python setup.py install
{% endcodeblock %}

３.安装好了就可以初始化gitosis，还得先建立一个git的用户来做一些工作：  


{% codeblock %}
useradd -m -s /bin/bash -d /home/git git
passwd git #给git用户加上密码
su - git
cd ~
gitosis-init < /tmp/id_rsa.pub #这里是你的rsa共钥路径
{% endcodeblock %}

４.修改一些权限，据说很重要，为了安全：  


{% codeblock lang:bash %}
chmod 755 /home/git
chmod 700 /home/git/.ssh
chmod 644 /home/git/.ssh/authorized_keys 
chmod 755 /home/git/repositories/gitosis-admin.git/hooks/post-update 
{% endcodeblock %}

５.在本地用git做最后的工作，修改gitosis的配置文件并上传：  


{% codeblock lang:bash %}
git clone ssh://git@DOMAIN:8888/gitosis-admin.git
cd gitosis-admin
vi gitosis.conf
#增加新的项目名字和相关配置
[group AWAD]#ＡＷＡＤ组
writable = wodeyitian_web　　　#仓库中的名字
members = dawncold@tianzhenmatoMacBook-Pro.local　　#成员，这里的成员名字就是rsa共钥中最后的成员名字
{% endcodeblock %}

好像和那个pub文件的名字要一样，那样的pub文件放在和这个conf文件在一起的keydir文件夹下. 

6.完成这里后提交一下再push到远程服务器上即可完成：  

{% codeblock lang:bash %}
git commit -a -m '建立了新的项目'
git push
{% endcodeblock %}

7.已经全部完成，在本地已经可以用了，不过还想说一下，如果做开源项目，还是放到github上比较好玩！
