---
layout: base
permalink: /note/2017-06-14-00
title: NSURLSessionConfiguration与NSURLRequest中相同属性的优先级问题
---

根据[文档](https://developer.apple.com/documentation/foundation/nsurlsessionconfiguration)中的说法

> <span style="font-size:30px;color:black">Note</span>
>
> In some cases, the policies defined in this configuration may be overridden by policies specified by an NSURLRequest object provided for a task. Any policy specified on the request object is respected unless the session’s policy is more restrictive. For example, if the session configuration specifies that cellular networking should not be allowed, the NSURLRequest object cannot request cellular networking.

一些情况下~~(妈的一些情况到底是哪几种情况你倒是说清楚啊)~~，NSURLRequest的属性优先级高于NSURLSessionConfiguration

不过如果是限制型的属性，则是NSURLSessionConfiguration的优先级高

比如allowsCellularAccess，如果在NSURLSessionConfiguration中设置了不能使用蜂窝网络，那么NSURLRequest及时设置了可以一样不行