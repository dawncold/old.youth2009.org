---
layout: post
title: "external disk with openwrt"
date: 2014-08-22 23:05:57 +0800
comments: true
categories: study
---

上次笔记本替换下来的硬盘闲在那里很久了，反正闲着没用，不如装点东西，比如监控的图片什么的，每分钟两张的速度拍，一个工作日，大约能有5G的数据，要是都传到七牛那么也就两天，免费的磁盘空间就满了，但绝大多数图片是没意义的，手动删的话，勤快些也行。

不过要是存到磁盘上的话，就无所谓了，500G的空间，怎么能等好几个月之后再考虑，程序员都是很懒很懒的。。。

磁盘是笔记本的2.5英寸STAT接口，需要一根USB2STAT的线，接到已经很疲劳的路由器上（703N改装版），路由器刷了OpenWrt。

登陆路由器后需要装几个软件，一是mount磁盘需要的，二是vsftpd，准备做成ftp供监控使用。把磁盘连接到路由器上而不是直接连到监控上的原因是：假如有人入侵，看到监控一定会破坏，有可能会把磁盘也带走，这样证据就木有了，而连接到路由器上的话，位置比较隐蔽，不容易察觉，会好一些，我就是这么邪恶。。。

对于mount磁盘需要的软件可能是：
{% codeblock %}
opkg update
opkg install kmod-usb-storage block-mount kmod-fs-ext4
{% endcodeblock %}
可能不是必须的，但看了文档没怎么研究，反正装了这些能mount了，由于我就一块磁盘，直接mount到了/mnt中。

{% codeblock %}
mount /dev/sda1 /mnt
{% endcodeblock %}
能用后需要把/mnt的owner改为`root:root`，权限755，在/mnt下创建ftp目录，owner是`ftp:ftp`，权限755。（ftp用户是装了vsftpd后创建的，所以你需要先装一下vsftpd）

vsftpd的配置：

{% codeblock %}
background=YES
listen=YES
anonymous_enable=NO
chroot_local_user=YES
local_enable=YES
local_root=/mnt
write_enable=YES
local_umask=022
check_shell=NO
{% endcodeblock %}
研究了一段时间这些配置，第一个建议测试时候用NO，正式开始用就YES，否则会让路由器一直卡在启动vsftpd这里，网路会不可用。比较关键的是`local_root`，登陆后用户的root目录会在这里，但不能在里面的ftp中，原因和chroot有关，刚刚在/mnt中创建的ftp目录就是ftp用户登陆上去后可操作的地方，所有操作都需要在ftp目录下进行。其他配置具体不详述，具体含义可以看官方的man page，感觉前七行是比较重要的。

ftp搭建过程中出现can not create file和permission方面的问题请检查local_root和里面目录的权限。另外vsftpd有本地用户和匿名用户、虚拟用户等不同的配置，我用的是本地用户的方法，其他两种，除了虚拟用户配置看起来比较麻烦我没有尝试外，匿名用户也配置过，不过后来一直卡在can not create file这里，没再尝试，应该还是权限问题。

下面是OpenWrt启动mount的设置，在`/etc/config/fstab`中加入：

{% codeblock %}
config mount
	option target /mnt
	option device /dev/sda1
	option fstype ext4
	option options rw,sync
	option enabled 1
	option enabled_fsck 0
{% endcodeblock %}
具体的/mnt和/dev/sda1、ext4根据你的情况做修改，enabled为1就是启动时加载。

没想到的是装了vsftpd，又挂了个磁盘，小路由器还能撑得住，也许还没开始用，等往里写文件的时候再看看。