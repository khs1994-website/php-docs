---
title: Monolog -- PHP 日志库
date: 2018-03-27 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Library
---

官方网站：https://seldaek.github.io/monolog/

GitHub：https://github.com/Seldaek/monolog

<!--more-->

```bash
$ composer require monolog/monolog
```

```php
// create a log channel
$log = new Logger('name');
$log->pushHandler(new StreamHandler('/path/to/your.log', Logger::WARNING));

// add records to the log
// 之后只能调用 warning 以上级别
$log->warning('Foo');
$log->error('Bar');
```
