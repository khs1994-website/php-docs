---
title: PHP7 配置详解
date: 2017-05-07 13:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

# PHP-FPM后台执行

```bash
daemonize = yes
```

<!--more-->

# macOS

```bash
$ brew install php71
# shell 脚本 ，建议使用以下命令 启动、停止、重启 php-fpm
$ php71-fpm {start|stop|force-quit|restart|reload|status|configtest}
```
