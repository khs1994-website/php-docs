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

**部分列出**

# 类型申明

函数参数、返回值

`string` `int` `float` `bool` + `类名` `接口` `数组` `回调类型`

# null 合并运算符 `??`

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

# `define` 可定义常量数组

# use 分组

```php
use some\namespace\{
      ClassA,
      ClassB,
      ClassC as C
    };
```

# 匿名类
