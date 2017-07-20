---
layout: base
permalink: /note/2015-02-06-03
title: simditor以及highlight.js
---

首先是simditor的使用

这个很容易（附链接：[Simditor使用方法](http://simditor.tower.im/docs/doc-usage.html)）

然后就是搭配simditor实现代码高亮的效果

首先simditor编辑的内容都要放到pre标签里

代码部分的格式是这样的：
    
    <html>
    <div class="lang-c++ selected" data-lang="c++">
    </html>

而highlight.js提供的高亮的功能

我们只要把对应代码位置的class类型改成hightlight.js要求的格式就好了

这是google到的一份实现以上功能的js代码（附链接：使用simditor作为django的富文本编辑器）：

    <html>
    <script type="text/javascript" src="/static/js/highlight.js"></script>
    <script>
    $(document).ready(function(){
            $("pre[class^='lang']").each(function(i, block){
                hljs.highlightBlock(block);    
            });
            hljs.initHighlightingOnLoad();  // 加这句是为了兼容之前的。
    });
    </script>
    </html>

就酱