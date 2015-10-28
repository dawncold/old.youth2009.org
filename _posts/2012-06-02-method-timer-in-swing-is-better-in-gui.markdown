---
layout: post
title: swing中的Timer还是用在GUI中的好
comments: true
date: 2012-06-02 09:23
categories: java study
---

刚刚翻了翻《Java核心技术》这本书，里面提到了swing中的Timer的用法，我就实践一下，结果发现根本没有反映，于是网上搜索答案，在stackoverflow中找到。

我写的测试是每秒输出现在的时间而已。


{% codeblock lang:java %}
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Date;


public class TimePrint implements ActionListener
{

   @Override
   public void actionPerformed(ActionEvent e)
   {
       // TODO Auto-generated method stub
       System.out.println("date is: " + (new Date()));
       Toolkit.getDefaultToolkit().beep();
   }
}

{% endcodeblock %}

在调用的时候如果忘记写Thread.sleep(xxx)这行就不会看到效果，具体原因不太清楚，可能这个swing中的Timer只是用来在GUI中做些什么工作的，而我用终端输出内容就不太合适了，于是就牵扯出来很多线程的问题。

这是main方法中的内容：


{% codeblock lang:bash %}
import java.awt.event.ActionListener;

import javax.swing.Timer;


public class TimerPrintTest
{
   public static void main(String[] argStrings) throws InterruptedException
   {
       System.out.println("Running...");
       ActionListener listener = new TimePrint();
       Timer timer = new Timer(1000, listener);
       timer.start();
       Thread.sleep(4000);
   }
}

{% endcodeblock %}
