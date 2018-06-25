---
layout: base
permalink: /note/2016-08-10-00
title: 关于cocoapods里pod编译的问题
---

前一段时间公司的APP要支持webp格式的图片

所以引入了SDWebImage的子模块WebP

WebP模块有一个UIImage的扩展

内容大概是这样（去掉了一些不相关的代码）

    #ifdef SD_WEBP

    #import <UIKit/UIKit.h>

    @interface UIImage (WebP)

    + (UIImage *)sd_imageWithWebPData:(NSData *)data;

    @end

    #endif

也就是说这个头文件会检查是否有SD_WEBP这个宏定义

如果有才会声明这个类方法（当然.m文件中也有类似的处理）

业务线的代码都是作为Pod引入的

当时在eLongHome这个Pod中使用了这个类方法

然后问题来了

编译失败

报错是没有找到这个方法

我勒个去

SD_WEBP的声明不是已经自动添加了么

为毛还会有这个错误

之后我对这个问题研究了几天

得出了一下成果：

### cocoapods对每个Pod都是单独编译然后把所有的Pod打包成一个libPods.a文件

在对使用了这个类方法的文件进行编译的时候

编译器发现这个类方法是需要SD_WEBP这个宏定义的

然后去当前文件所引用的宏定义里去找

主要有这么几个位置

> 1.当前文件中的声明，即在这个.m文件里的define语句

> 2.当前文件所引用的.h文件（包括引用的.h文件引用的头文件，依次往上查找，能找到就算），这个.h文件位置随意，可以在其他Pod中

> 3.Pod的工程文件中，该Pod所对应的target中的Building Settings中的宏定义设置（Preprocessor Macros）

只要在这几个位置有SD_WEBP的声明，就可以编译通过



不过我仔细想了一下

既然是单独编译的

那不是只要SDWebImage在编译的时候能找到SD_WEBP这个宏定义不就可以了么

为什么必须要使用的位置也要声明

在经过一番思考之后我只得出了一个合法的猜测

> 使用该类方法时所声明的宏定义仅用于编译检查，与实际使用无关（也就是说其实是可以执行的只是编译不给过）
验证的过程也非常简单

OC本身有runtime的特性

用performSelector绕过编译检查就可以了

实际结果证明了我的猜测是正确的



在探索的过程中还有一个细节是我以前没有注意到的

那就是预处理命令是有顺序的

这些写法是合法的

    1.
    #define SD_WEBP 1
    #import "UIImage+WebP.h"

    2.
    #import "Test.h"            // Test.h中有SD_WEBP的宏定义或者Test.h所引用的头文件中有，依次往上查找能找到就算
    #import "UIImage+WebP.h"

这些写法是不合法的

    1.
    #import "UIImage+WebP.h"
    #define SD_WEBP 1

    2.
    #import "UIImage+WebP.h"
    #import "Test.h"            // Test.h中有SD_WEBP的宏定义或者Test.h所引用的头文件中有，依次往上查找能找到就算

以上