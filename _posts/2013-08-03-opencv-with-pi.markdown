---
layout: post
title: "opencv-with-pi"
date: 2013-08-03 17:44
comments: true
categories: raspberrypi
---

想了好久都觉得连续拍照片做监控实在是没什么效率，默认情况应该是什么都不做，如果发现有人来了才拍下来或者录下来，但用标配的摄像头录像实在是会录出非常大的文件，保存文件又是问题。在[官网的博客](http://www.raspberrypi.org/archives/4207)中看到了一个用opencv做的人脸识别，可以这样干嘛。于是紧随那片文章开始干。

由于标配摄像头模块不是usb设备，所以需要重新编译使用的几个程序，比如raspistill和raspivid等等。

另外，如果直接在raspberrypi上编译，需要安装一些软件：[http://thinkrpi.wordpress.com/2013/04/05/step-3-install-softwares-for-webcam-and-computer-vision/](http://thinkrpi.wordpress.com/2013/04/05/step-3-install-softwares-for-webcam-and-computer-vision/)

具体的操作请参照：[http://thinkrpi.wordpress.com/2013/05/22/opencv-and-camera-board-csi/](http://thinkrpi.wordpress.com/2013/05/22/opencv-and-camera-board-csi/)

替换arm-linux.cmake的命令:`sed -i 's/if (DEFINED CMAKE_TOOLCHAIN_FILE)/if (NOT DEFINED CMAKE_TOOLCHAIN_FILE)/g' arm-linux.cmake`，看准了arm-linux.cmake的路径，我运行命令的时候已经到了和arm-linux.cmake一个目录下了。