---
layout: post
title: VPS中部署了Flask框架
comments: true
date: 2012-07-02 20:46
categories: python vps
---

一开始我也是用web.py的，不料接受不了它的session处理，然后离开，Django这种庞大的东西我是没精力去研究了，当然开始也伴随激情看过文档，没坚持下去，后来和强锅一起找了不少框架做东西，我实践性比较强，就找到了Flask，感觉还挺好用的，做了一个todo，有兴趣可以看：http://todo.wodeyitian.com。

原先部署在dotcloud上，刚刚在自己的VPS上完成了nginx+uwsgi+flask的集成，当然还是没有废弃掉php，为了好几个博客嘛～

总的来说就是用virtualenv来创建各个app的目录，在里面安装需要的环境（flask、mysql-python、beautifulsoup4等等吧），nginx的配置大概如下：


{% codeblock lang:bash %}
server {
     listen       80;
     server_name  todo.wodeyitian.com;
     location / {
               include uwsgi_params;
               uwsgi_pass 127.0.0.1:9090;
               uwsgi_param UWSGI_PYHOME /home/wwwroot/python_app_todo;
               uwsgi_param UWSGI_CHDIR /home/wwwroot/python_app_todo/app_dir;
               uwsgi_param UWSGI_SCRIPT todoApp:app;
     }
}
{% endcodeblock %}

UWSGI_PYHOME是app的主目录，下面的CHDIR是app中py文件所在的目录，这个可以自己设置，下面的SCRIPT是入口脚本模块名和变量名，模块就是文件名喽，变量一般在flask都是用app作为整个网站的入口变量，写过python基本都能明白这个。

安装好uwsgi后可以配置开启：


{% codeblock lang:bash %}
uwsgi -s :9090 -M -p 4 -t 30 --limit-as 128 -R 10000 -d uwsgi.log --vhost
{% endcodeblock %}

使用9090端口监听，-M开启主控线程，-p 4是开启4个线程，-t 30是超过30秒不响应丢弃，limit-as 128是限制128Mb的内存占用，-R 10000是超过10000的请求就自动respawn（似乎是自动复制？重启？之类的），-d是日志，--vhost这个可以让多个app共用一个uwsgi，很好用的！