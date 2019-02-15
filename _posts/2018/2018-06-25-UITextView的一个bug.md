---
layout: base
permalink: /note/2018-06-25-00
title: UITextView的一个bug
---

最近在重构公司APP用的debugView

发现UITextView的editable属性设置为NO时

使用scrollRangeToVisible方法会改变textContainer的区域

![](/img/2018/UITextView的一个bug_0.png?raw=true)

![](/img/2018/UITextView的一个bug_1.png?raw=true)

解决办法是将UITextView的layoutManager属性的allowsNonContiguousLayout设置为NO

即

    textView.layoutManager.allowsNonContiguousLayout = NO;
