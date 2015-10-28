---
layout: post
title: "got-raspberry"
date: 2013-08-02 21:40
comments: true
categories: life raspberrypi
---

工资一发就买了块表。。。并且还狠心买了这个玩具——raspberry。

默认用了新手的那个镜像，叫NOOBS，就是里面装好了不少东西，系统也有好几个，默认用了推荐的Raspbian，是Debian的一个变种啦，开发用的Ubuntu都是一个家族的。

配置的话，没啥可说的，就是把显卡占用的内存改成了16Mb，默认似乎分配了128M过去，对于我这种总看命令行的人足够了。如果你和我一样买了官方的摄像头模块，那就可以把camera给enable了。再就是在adcanced options中把SSH打开，否则你还得连上键盘鼠标去操作。。。

不喜欢插网线，但很可惜办公室的Cisco双频无线网卡AE2500装不上，貌似是驱动问题，不想折腾，还好买了个免驱的小网卡叫EOUP。我的无线路由是hidden SSID了，所以在连接的时候还有点问题。在配置文件`/etc/wpa_supp/wpa_supp.conf`中多加了一行：
`scan_ssid=1`

apt的source也改到了ustc.edu.cn的：`http://mirrors.ustc.edu.cn/raspbian/raspbian/`，具体就是把`/etc/apt/source.list`中第一行的URL改成上面那个即可。

camera的官方使用教程：[http://www.raspberrypi.org/archives/3890](http://www.raspberrypi.org/archives/3890)

如果想用camera捕捉视频，然后传到你这里看的话，需要在raspberry上先装netcat，我是用的Mac系统，系统本身有nc了，再用brew多装一个mplayer。

raspberrrypi上捕捉视频用：`raspivid -t 0 -vs -w 800 -h 600 -o -| nc 172.19.1.124 5001`，其中t参数指定了捕捉多少毫秒的视频，用0表示禁用这个选项，后面的vs是防抖，w和h控制宽高，这样就得到一个800x600的画面。

Mac上用nc把发来的stream转到mplayer上：<del>`nc -lp 5001 | mplayer -fps 31 -cache 512 -`</del>，很无语的是`man nc`得到一句解释，l和p参数在一起用是个错误，但只用l是不管用的，给作者发了封信问下，不知道会不会得到回信。

**2015-01-18:**今天有机会使用树莓派的视频功能，因为要监控看看麻麻什么时候从外面回家，于是找相关命令，想到自己以前用过这个，就找出来了，结尾算是遗留的一个尾巴，今天解决一下。

我给原作者发了邮件，可惜邮件被退了，又给IPV6版本的实现作者发信，还没回，后来给Ubuntu-dev的组发了信（是不是很大胆？），管理员回了我，告诉我不能在这问这种问题，不过说了一些东西，虽然没什么帮助，但我确实在ubuntu上试了下`nc -l IPADDRESS 5000`这条命令是否管用，还真能用，确实不应该加`-p`参数，但为何我这里的就不对呢？实际Mac系统本身有nc，后来我用brew装了个netcat，然后系统里面就有点乱了，卸载掉netcat后，直接用系统的nc，就和man中说的一样了，不用加`-p`，参数，实际是不应该加那个参数，而是`nc -l IPADDRESS 5000`，文中提到的那种写法我标记删除了。