---
layout: base
permalink: /note/2020-07-08-00
title: 【Cocoapods】记一个podspec写错的问题
---

今天发现了一个问题

有个podspec是这么写的

```ruby
s.resources = "Source/**/*.{xib,bundle,plist,json,gif,scnassets}"
```

这样会导致bundle下面的xib等匹配到其他后缀格式的文件单独添加到工程中

比如a.bundle下面有个b.json

这个b.json因为也满足这个匹配的格式

所以会单独添加到工程里

单独添加到工程里的这个既没有什么用还会打到包里

所以需要避免这种情况
