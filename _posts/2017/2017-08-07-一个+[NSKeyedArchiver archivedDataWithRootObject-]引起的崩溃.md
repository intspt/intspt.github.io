---
layout: base
permalink: /note/2017-08-07-00
title: 一个+[NSKeyedArchiver archivedDataWithRootObject:]引起的崩溃
---

话说我们框架里持久化数据的部分是我写的

有这么一句总有崩溃

    [NSKeyedArchiver archivedDataWithRootObject:self.userDefaultDict]

后来发现是因为这个方法内部会进行快速遍历

当userDefaultDict在其他线程刚好被修改的时候就会崩溃

解决办法就是传值的时候传copy