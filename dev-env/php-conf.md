---
title: PHP7 配置详解
date: 2017-05-06 13:00:00
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

# PHP-FPM后台执行

```bash
daemonize = yes
```

# macOS

```bash
$ brew install php71
# shell 脚本 ，建议使用以下命令 启动、停止、重启 php-fpm
$ php71-fpm {start|stop|force-quit|restart|reload|status|configtest}
```
