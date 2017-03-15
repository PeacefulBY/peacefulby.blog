---
title: 新Mac安装软件
id: 241
categories:
  - 未分类
tags:
---

1、brew

Mac 安装软件，相当于apt-get or wget，安装地址：http://brew.sh

&nbsp;

2、Shadowsocks

开源翻墙软件，包括服务器端和客户端，github：https://github.com/shadowsocks/

服务器端安装包括命令：

sudo ssserver -p 8388 -k 19077336 -m aes-256-cfb -d start

&nbsp;

shadowsocks是sock5代理，通过http代理访问要使用privoxy：http://sourceforge.net/projects/ijbswa/files/

&nbsp;