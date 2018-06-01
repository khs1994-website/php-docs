---
title: PHP7 配置详解
date: 2016-09-22 13:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

本文简要介绍了 PHP 常用配置。

<!--more-->

# PHP-FPM

## PHP-FPM 后台执行

```bash
daemonize = yes
```

忽略配置文件，通过命令方式指定后台或前台运行。

```bash
$ sudo php-fpm -D | -F
```

## 进程数量管理方式

```bash
pm = dynamic | static | ondemand

; static 静态，固定数量 ( pm.max_children )的子进程

; dynamic 动态 最大数量、启动时数量 ( pm.start_servers )、空闲状态下的最小、最大进程数量 (pm.min_spare_servers)

; ondemand 当有连接时启动进程，闲置 pm.process_idle_timeout 秒后杀掉进程。
```

队列长度

```bash
listen.backlog
```

最大请求数优化，指一个 php-fpm 的工作进程在处理多少个请求后就终止掉

```bash
pm.max_requests
```

最长执行时间

```bash
request_terminate_timeout
```

# `php.ini`

* 变更历史：https://github.com/php/php-src/commits/master/php.ini-development

* `php.ini` 中文版：http://www.jinbuguo.com/php/php52-ini.html
