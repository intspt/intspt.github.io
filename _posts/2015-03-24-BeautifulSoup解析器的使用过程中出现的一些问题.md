---
layout: base
permalink: /note/2015-03-24-00
title: BeautifulSoup解析器的使用过程中出现的一些问题
---

今天写爬虫爬小说的时候用BeautifulSoup解析网页出现了一些问题

一开始解析章节总是错误然后很费解

后来发现是在生成BeautifulSoup对象时丢失了后边一大部分数据

卧槽尼玛这TM是什么情况

我一开始以为有长度限制

不过文档里没说也没google到

再说长度限制什么的有点扯。。。

后来google到一个相似的问题

[BeautifulSoup / lxml: Are there problems with large elements?](http://stackoverflow.com/questions/16029442/beautifulsoup-lxml-are-there-problems-with-large-elements)

根据回答里的建议把lxml改成了html.parser就好了

当然只是解决问题我肯定是不满足的

后来继续寻找原因

发现是编码的问题

我一开始是把网页用utf-8解码之后才生成BeautifulSoup对象

于是这里出现了一些问题

解码之后的文件中出现了很多反斜杠【utf-8编码带来的

然后这使得网页格式出现了一些问题【有些标签未闭合

后来发现文档里有这么一句

> 首先,文档被转换成Unicode,并且HTML的实例都被转换成Unicode编码

因此对于utf-8格式的网页不需要解码编码直接传入即可