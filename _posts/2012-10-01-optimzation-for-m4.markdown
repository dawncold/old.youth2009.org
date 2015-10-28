---
layout: post
title: M4的一点优化(MacOS 10.9)
comments: true
date: 2012-10-01 17:05
categories: mac ssd
---
1.关闭紧急运动传感器

mac系统没有把这些传感器的设置、界面什么的体现到UI里，让我一度以为mbp没有这种设备，实际这也算是mac系统的设计理念吧，把普通用户无须知晓的东西屏蔽掉，让用户看起来、用起来异常简单，不像thinkpad那样，直接把硬盘活动保护啥的做成一个功能给用户展示。。。你看，你看，我们（thinkpad）有保护您硬盘的设备。

这些不让用户看到的功能大多需要相关工具或者命令行来设置：
{% codeblock lang:bash %}
sudo pmset -a sms 0
{% endcodeblock %}

对于替换了原来硬盘的这种方案就可以关闭紧急运动传感器了，如果加了SSD在光驱位，那就甭管了，继续保护硬盘吧！


2.备份驱动

{% codeblock lang:bash %}
sudo cp /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/MacOS/IOAHCIBlockStorage /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/MacOS/IOAHCIBlockStorage.original
{% endcodeblock %}

3.更新驱动

{% codeblock lang:bash %}
sudo perl -pi -e 's|(\x52\x6F\x74\x61\x74\x69\x6F\x6E\x61\x6C\x00{1,20})[^\x00]{9}(\x00{1,20}\x54)|$1\x00\x00\x00\x00\x00\x00\x00\x00\x00$2|sg' /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/MacOS/IOAHCIBlockStorage
{% endcodeblock %}

4.开启Trim

{% codeblock lang:bash %}
sudo kextcache -system-prelinked-kernel
{% endcodeblock %}

5.清除系统内核扩展缓存

{% codeblock lang:bash %}
sudo kextcache -system-caches
{% endcodeblock %}

6.重启

如果出错就恢复刚刚的备份

{% codeblock lang:bash %}
sudo cp /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/MacOS/IOAHCIBlockStorage.original /System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/MacOS/IOAHCIBlockStorage
{% endcodeblock %}

3.用noatime方式挂载硬盘，就是少加载一个文件属性参数而已，对于日常使用没啥影响，在/Library/LaunchDaemons里面创建一个noatime.plist，内容如下：

{% codeblock lang:xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
"http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>Label</key>
<string>noatime</string>
<key>ProgramArguments</key>
<array>
<string>mount</string>
<string>-vuwo</string>
<string>noatime</string>
<string>/</string>
</array>
<key>RunAtLoad</key>
<true/>
</dict>
</plist>
{% endcodeblock %}

修改刚刚创建的文件权限

{% codeblock lang:bash %}
sudo chown root:wheel /Library/LaunchDaemons/noatime.plist
{% endcodeblock %}

重启

检测结果

{% codeblock lang:bash %}
mount | grep " / "
{% endcodeblock %}

如果结果里有类似这样的内容（最后的noatime）就表示可以了

{% codeblock lang:bash %}
/dev/disk0s2 on / (hfs, local, journaled, noatime)
{% endcodeblock %}
