---
layout: base
permalink: /note/2020-04-01-00
title: 【Flutter】Row的Child实现不同的alignment
---

    好久没记笔记了 
    不是说没什么可写的 
    只是自己越来越懒了 
    今年补一下吧

Flutter里Row本身具有一个alignment属性

只是这个属性是全局的

一改就都改了

最近有个地方需要给不同的Child设置不同的alignment

发现可以这么解

首先设置Row的crossAxisAlignment属性为CrossAxisAlignment.stretch

然后将每个Child都用Container包一下

将Container的alignment属性设置为想要的alignment就可以了