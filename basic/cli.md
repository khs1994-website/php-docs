---
title: PHP CLI
date: 2018-08-07 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

PHP CLI 模式下简介。

<!--more-->

# 长时间执行

* https://github.com/khs1994-docker/lnmp/issues/484

```php
Fatal error: Maximum execution time of 30 seconds exceeded

ini_set('max_execution_time', '0');

set_time_limit(0);
```

# 多进程

`pcntl_*` 系列函数。
