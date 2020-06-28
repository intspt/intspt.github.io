---
layout: base
permalink: /note/2020-06-28-00
title: 【shell】libimobiledevice常用功能
---

最近发现了一个很强大的工具叫[libimobiledevice](https://github.com/libimobiledevice/libimobiledevice)

这个库的功能很多

我就不一一列举了

这里主要讲下我常用的几个功能

# 模拟定位

这个之前说过了

直接看[这个](https://intspt.github.io/note/2020-06-17-00)就行

# 查看控制台输出

这功能跟直接用Mac自带的控制台查看手机控制台的输出是一样的

不过这个有高亮

看起来更舒服

而且还可以按进程名称筛选

比如下面的命令就可以查看SpringBoard这个进程的实时日志

如果APP在还未启动就闪退这个进程就会输出报错的日志【比如描述文件过期的情况】

```bash
idevicesyslog -p SpringBoard
```

# 导出手机上的崩溃日志

这个崩溃日志指的是系统手机的那个

就是在设置 -> 隐私 -> 分析与改进 -> 分析数据里的那些东西

这个里面的东西手机上是没法直接删除的

所以会越来越多

耽误我们查看最新的崩溃日志

导出的命令也很简单【注意tmp文件夹要自己先创建】

导出之后手机上的日志就没了

这功能Xcode也有

只是我觉得这个命令更方便

```bash
idevicecrashreport -e tmp
```