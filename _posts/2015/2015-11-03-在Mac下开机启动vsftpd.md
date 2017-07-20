---
layout: base
permalink: /note/2015-11-03-00
title: 在Mac下开机启动vsftpd
---

vsftpd的搭建就不多说了

随便搜一下一大堆

但是Mac下开机启动vsftpd这个比较难搜到【我没搜到

一开始搞了好久没成功

后来发现主要原因是

vsftpd必须要以root身份启动

所以不能放在家目录下的Library/LaunchAgents/路径下

必须要放在系统的/Library/LaunchDaemons/路径下才行

当然权限也必须要对