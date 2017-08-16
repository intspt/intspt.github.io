---
layout: base
permalink: /note/2017-08-16-00
title: proxychains-ng执行系统命令时的错误
---

最近用brew安装一个软件包的时候用proxychains-ng走了代理

结果报了这么个错

    dyld: warning: could not load inserted library '/usr/local/Cellar/proxychains-ng/4.12_1/lib/libproxychains4.dylib' into library validated process because no suitable image found.  Did find:
        /usr/local/Cellar/proxychains-ng/4.12_1/lib/libproxychains4.dylib: code signing blocked mmap() of '/usr/local/Cellar/proxychains-ng/4.12_1/lib/libproxychains4.dylib'

查了一下大佬回答说是系统命令就会这样

> It only happens if you execute a system binary using proxychains, e.g. proxychains4 ssh user@server. For now, a workaround is to copy the executable to another location (e.g. cp /usr/bin/ssh ~/XXX), and use it (e.g. proxychains4 ~/XXX/ssh user@server). You can modify the path variable so that ~/XXX/ssh is executed instead of /usr/bin/ssh, when you just type "ssh".

跟rootless有关

不过似乎也不影响执行

而且我觉得这么做复制挺蠢的

所以就这样吧