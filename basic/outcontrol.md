---
title: PHP 输出控制
date: 2018-05-27 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

本文介绍 PHP `ob_*` 系列函数。

<!--more-->

`ob_flush` 是刷新 PHP 自身的缓冲区

`flush` 只有在 PHP 做为 apache 的 Module 安装的时候, 才有实际作用.它是刷新 WebServer (可以认为特指 apache )的缓冲区.

正确使用俩者的顺序是. 先 ob_flush, 然后 flush, 为了保证你代码的可移植性, 建议配套使用。

NGINX 可以增加响应头 `header('X-Accel-Buffering: no');`
