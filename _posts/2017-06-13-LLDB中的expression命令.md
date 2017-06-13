---
layout: base
permalink: /note/2017-06-13-00
title: LLDB中的expression命令
---

先看一下print跟po

## print

> ('expression --')  Evaluate an expression on the current thread.  Displays any returned value with LLDB's default formatting.  Expects 'raw' input (see 'help raw-input'.)
>
> Syntax: print <expr>
>
> Command Options Usage:
>   print <expr>
>
> 'print' is an abbreviation for 'expression --'

## po

> Evaluate an expression on the current thread.  Displays any returned value with formatting controlled by the type's author.  Expects 'raw' input (see 'help raw-input'.)
>
> Syntax: po <expr>
>
> Command Options Usage:
>   po <expr>
>
> 'po' is an abbreviation for 'expression -O  --'

显然这俩命令都是基于expression并且做了一些简单的定制【我一直以为print就是单纯的输出，po就是print object...

然后再看看expression

## expression

> Evaluate an expression on the current thread.  Displays any returned value with LLDB's default formatting.  Expects 'raw' input (see 'help raw-input'.)
>
> Syntax: expression <cmd-options> -- <expr>
>
> 后面还有很多就不贴了

# 结论

> expression是一个执行并输出返回结果的命令，并且输出可以定制
>
> print基于expression，不接受定制输出的参数
>
> po基于expression，不接受定制输出的参数
>
> print一般用于输出基础的数据类型
>
> po一般用于输出对象【优先调用debugDescription，其次调用description