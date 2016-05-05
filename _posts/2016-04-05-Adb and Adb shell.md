---
layout: post
title: Adb and Adb shell
category: Technology
comment: true
---

**Adb and Adb shell**

[adb shell命令详解](http://blog.163.com/hero_213/blog/static/3989121420115915014721/)

[adb logcat命令](http://blog.csdn.net/hansel/article/details/38088583)

Android手机经常通过adb抓取main log和 kernerl log，
main log命令：adb logcat -v time > main.log
kernel log命令：adb shell cat /proc/kmsg > kmsg.log。
在USB无法使用的情况下，诸如charger问题，只能用UART抓取log。
MTK平台Android手机还可以通过GAT工具抓取log：[如何用GAT抓取log](http://blog.csdn.net/lxl584685501/article/details/45483153)。

[adb常用命令合集](http://blog.csdn.net/liu_chunhai/article/details/7463420)

[adb常用命令略解](http://www.cnblogs.com/ccxniit2004/archive/2012/02/13/2349767.html)

**END**
