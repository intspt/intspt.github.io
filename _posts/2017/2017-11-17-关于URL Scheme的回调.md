---
layout: base
permalink: /note/2017-11-17-00
title: 关于URL Scheme的回调
---

    - (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url;
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation;
    - (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey, id> *)options;

关于URL Scheme唤起的回调目前总共有这么三个

其中第一个是最早的(2.0)

第二个稍晚一些(4.2)

最后一个是最新的(9.0)

优先级上最后一个 > 第二个 > 第一个