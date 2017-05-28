---
layout: base
permalink: /note/2017-04-25-00
title: OC中引用高版本才有的framework的问题
---

如果你引用了一个低版本没有的framework

并且import了它的头文件

但是没有使用

低版本不会报错

如果需要在高版本上使用该framework

以optional的形式引用(podspec里写成weak_framework)

正常导入头文件

在使用时进行版本判断即可

低版本不会报错