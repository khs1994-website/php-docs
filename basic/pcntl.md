---
title: PHP 多进程 pcntl
date: 2018-06-03 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

`pcntl_*` 系列函数介绍。

<!--more-->

`$pid = pcntl_fork()` 之后，当前进程和 `fork` 出来的子进程同时执行。

我们通过判断 `$pid` 来判断当前进程是哪个进程。

`$pid` 为 0 时为子进程，`$pid` 为 `-1` 时子进程创建失败。其他为当前进程。

`pcntl_wait()` 等待或返回 fork 的子进程状态

`pcntl_wifexited()` 检查子进程状态代码是否代表正常退出
