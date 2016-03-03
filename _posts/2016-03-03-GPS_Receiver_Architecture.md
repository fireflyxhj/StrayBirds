---
layout: post
title: GPS Receiver Architecture
category: Technology
comments: true
---

#**GPS Receiver Architecture**
***
##**GPS Receiver Architecture**
[GPS接收机的灵敏度分析](http://blog.sina.com.cn/s/blog_4cd5dc1c0100yw2l.html)
***
##**几个公式**
扩频系统的灵敏度S=KTB+Eb/No+NF-Gp
***
GPS RF BW: 2.046 MHz
Modulation: BPSK
Process Gain: 46 dB
Thermal Noise Floor: kTB = -111 dBm/2.046MHz
Required Eb/N0: 6 dB (不太清楚, 可以修正)
Receiver NF: 3 dB (Typical)
***
S=-111+Eb/No+NF-Gp=-111 + 6 + 3 - 46 = -148 dBm
***
S=-KT+C/N0+NF=-174+23+3=-148
