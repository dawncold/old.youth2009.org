---
layout: post
title: 9个数运算结果为110
comments: true
date: 2012-04-08 14:20
categories: algorithm
---

昨天参加了一个小型编程比赛，有个题目是这样的，有1～9这九个数字，按照顺序排列着，你可以在他们之间加入加号、减号或者什么都不加，组成的算式经过运算后结果为110的输出出来。

看着好简单的题目，当时比赛时候就是一下子没做出来，现在做好了，贴出来，如果有需要可以拿去用哈，代码风格不算好，因为是比赛嘛，又不是商业项目，先快速得到结果再说！

{% codeblock lang:java %}
import java.util.ArrayList;


public class unittest
{
   public static void main(String[] argStrings)
   {
       long start = System.currentTimeMillis();
       ArrayList<String> allopts = new ArrayList<String>();
       int a,b,c,d,e,f,g,h;
       for(a = 0;a < 3;a++)
           for(b = 0;b < 3;b++)
               for(c = 0;c < 3;c++)
                   for(d = 0;d < 3;d++)
                       for(e = 0;e < 3;e++)
                           for(f = 0;f < 3;f++)
                               for(g = 0;g < 3;g++)
                                   for(h = 0;h < 3;h++) {
                                       allopts.add(""+a+b+c+d+e+f+g+h);
                                   }
       
       for (String string : allopts)
       {
           String base = "1x2x3x4x5x6x7x8x9";
           for (int i = 0; i < string.length(); i++)
           {
               String tmp = getOpt(Integer.parseInt(""+string.charAt(i)));
               base = base.replaceFirst("x", tmp);
           }
           int x = getResult(base, string.replaceAll("2", "").replaceAll("0", "+").replaceAll("1", "-"));//2->null
           if (x == 110)
           {
               System.out.println(base);
           }
       }
       System.out.println("All Run Time: " + (System.currentTimeMillis() - start) + "ms");
   }
   
   public static String getOpt(int opt) {
       String retString = "";
       switch (opt)
       {
           case 0:
               retString = "+";
               break;
           case 1:
               retString = "-";
               break;
           case 2:
               retString = "";
               break;
           default:
               break;
       }
       
       return retString;
   }
   
   public static int getResult(String calculatString, String optString)
   {
       ArrayList<Integer> allNum = new ArrayList<Integer>();
       ArrayList<String> allOpt = new ArrayList<String>();
       for (String string : calculatString.split("[+-]"))
       {
           allNum.add(Integer.parseInt(string));
       }
       for (int i = 0; i < optString.length(); i++)
       {
           allOpt.add(optString.charAt(i) + "");
       }
       int result = allNum.get(0);
       for (int i = 1; i < allNum.size(); i++)
       {
           char x = (i - 1) == allOpt.size()?'+':allOpt.get(i - 1).charAt(0);
           int nextNum = i == allNum.size()?0:allNum.get(i);
           result = getValue(result, nextNum, x);
       }
       
       return result;
       
   }
   
   public static int getValue(Integer num1, Integer num2, char opt)
   {
       int ret = 0;
       switch (opt)
       {
           case '+':
               ret = num1 + num2;
               break;
           case '-':
               ret = num1 - num2;
               break;
           default:
               break;
       }
       
       return ret;
   }
}
{% endcodeblock %}

结果是这样的：

{% codeblock lang:bash %}
1+2+34+5+67-8+9
1+234-56-78+9
1-2+3+45-6+78-9
12+3+45+67-8-9
12+34+56+7-8+9
12-3+4-5+6+7+89
123+4+5+67-89
123+4-5-6-7-8+9
123-4+5-6-7+8-9
123-4-5+6+7-8-9
All Run Time: 496ms
{% endcodeblock %}

最后我算了算运行时间，应该这就是很慢的了，幸好只有加减和空，要不然会更麻烦的……