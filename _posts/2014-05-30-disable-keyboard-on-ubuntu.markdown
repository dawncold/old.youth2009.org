---
layout: post
title: "disable-keyboard-on-ubuntu"
date: 2014-05-30 20:54:45 +0800
comments: true
categories: dev
---

有时候不接外置显示器的时候，喜欢把键盘压在笔记本键盘上方使用，但如果不禁用内置键盘的话就会有误操作的风险，所以这样做，利用ubuntu中的xinput

查看设备使用`xinput list`

{% codeblock lang:bash %}
⎡ Virtual core pointer                      id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=11   [slave  pointer  (2)]
⎜   ↳ Logitech USB-PS/2 Optical Mouse           id=12   [slave  pointer  (2)]
⎜   ↳ Logitech Unifying Device. Wireless PID:4004   id=13   [slave  pointer  (2)]
⎣ Virtual core keyboard                     id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ Acer CrystalEye webcam                    id=9    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=10   [slave  keyboard (3)]
{% endcodeblock %}
找到内置键盘，我这里是那个叫"AT Translated Set 2 keyboard"的，id是10，禁用使用：`xinput float 10`

如果再启用使用`xinput reattach 10 3`，3标识这个设备的master的id，从list的结果很容易看到从属关系。