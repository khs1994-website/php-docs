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

# `php.ini`

变更历史：https://github.com/php/php-src/commits/master/php.ini-development

php.ini 中文版：http://www.jinbuguo.com/php/php52-ini.html
