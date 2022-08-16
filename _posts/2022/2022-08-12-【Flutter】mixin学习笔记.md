---
layout: base
permalink: /note/2022-08-12
title: 【Flutter】mixin学习笔记
---

# 定义

懒得写了，直接看[官方文档](https://dart.cn/guides/language/language-tour#adding-features-to-a-class-mixins)

#### 先吐槽一下往上搜到的文章

Google一下dart mixin能搜到挺多文章的，我看过好几篇，这里贴一个中文的讲讲读后感

地址: https://zhuanlan.zhihu.com/p/67831976

我看完这篇文章（其他几篇我搜到的也一样）以后，还是没有搞懂一个问题:

#### 为什么要用mixin？

下面是文章里给的示例代码（其他几篇我看过的文章给的也差不多）

```dart
abstract class Animal {
}

mixin Run {
    run() {
        print('run');
    }
}

mixin Fly {
    fly() {
        print('fly');
    }
}

mixin Swim {
    swim(){
        print('swim');
    }
}

class Bird extends Animal with Fly {}
class Dog extends Animal with Run {}
class Fish extends Animal with Swim {}
class Frog extends Animal with Run,Swim {}
```

说实话看完这段代码的第一反应是为啥不整一个静态方法直接调？

假如有一个地方需要使用run这个方法，我觉得都没必要通过Dog类去调，直接调用一个静态的run方法不就行了？反正结果都是一样的。

于是我搜了一下Flutter的framework里的代码，看到了一个叫AnimationLazyListenerMixin的mixin

发现这个mixin是提供了成员变量以及对应的方法的，这就解释了前面的疑问

无状态的mixin方法在我看来没什么意义，本质跟类方法是一样的

全都是虚函数的mixin也没什么意义，还不如写一个abstract class，然后用的地方implements，语义上还更清晰

一个有意义的mixin一定提供了有状态的方法，相当于对类的补强

#### 更进一步的mixin

mixin从字面意思上来看是“混合”，既然是混合，那么mixin提供的方法以及成员变量跟本类必须要有相互访问的能力

目前看到了以下几种场景（理论上还有mixin单向访问本类的场景，不过感觉没啥实用价值，除非你想用mixin写埋点）

+ 本类单向访问mixin

刚才提到的AnimationLazyListenerMixin就属于这种，给本类提供了添加监听相关的能力，本类在需要的地方进行调用即可

+ 本类跟mixin相互访问

mixin想要访问本类，首先要引入on这个关键字，比如RestorationMixin就是

```dart
mixin RestorationMixin<S extends StatefulWidget> on State<S>
```

on后面关联的State有点类似于父类的概念，RestorationMixin内部可以像访问父类一样的去访问State

至于调用顺序什么的可以看上面的那篇文章，这里不展开了
