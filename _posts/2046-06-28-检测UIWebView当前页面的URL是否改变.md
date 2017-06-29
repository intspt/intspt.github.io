---
layout: base
permalink: /note/2017-06-28-00
title: 检测UIWebView当前页面的URL是否改变
---

最近在做一个需求

有个要求是当UIWebView展示首页时顶部展示订单按钮

当不在首页时展示回到首页按钮

由于有些情况下页面跳转不会调代理

所以我的想法是通过KVO来观察属性的变化【[KVO的原理](http://www.jianshu.com/p/559164d8dddc)

以此确定页面是否改变

不过可惜的是UIWebView大概内部没有调用过setter

所以监听request属性或者canGoBack都不好使

后来发现UIWebView还有一个scrollView属性

我猜测页面变化时scrollView的subViews也会变化

因此它的frame也一定会重新赋值

于是我监听了这个属性

并且在变化时检测UIWebView是否可以返回(canGoBack)

就可以了【虽然实现的不美观。。。不过没辙了