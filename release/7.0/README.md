---
title: PHP 7.0 新特性
date: 2015-10-01 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Release
---

GitHub：https://github.com/php/php-src/releases/tag/php-7.0.0

官方文档：http://cn2.php.net/manual/zh/migration70.php

<!--more-->

# null 合并运算符

如果变量存在且值不为 `NULL`， 它就会返回自身的值，否则返回它的第二个操作数。

```php
$a = $_GET['user'] ?? 'default';

$a = isset($_GET['user']) ? $_GET['user'] : 'nobody';
```

# 太空船操作符

当 `$a` 小于、等于或大于 `$b` 时它分别返回 -1、0 或 1

```php
echo 1 <=> 1; // 0
echo 1 <=> 2; // -1
echo 2 <=> 1; // 1
```
