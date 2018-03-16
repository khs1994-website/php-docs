---
title: PHP 7.1 新特性
date: 2016-10-01 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Release
---

GitHub：https://github.com/php/php-src/releases/tag/php-7.1.0

官方文档：http://cn2.php.net/manual/zh/migration71.php

<!--more-->

**部分列出**

可为空类型 `Nullable`

传入的参数或者函数返回的结果要么是给定的类型，要么是 null

```php
function testReturn(): ?string
{
    return 'elePHPant';
}
```

返回值声明为 void 类型的方法要么干脆省去 return 语句，要么使用一个空的 return 语句。 对于 void 函数来说，NULL 不是一个合法的返回值。

```php
public function FunctionName(): void
{
  return;
}
```

类常量可见性

一个 catch 可捕获多个异常，用 `|` 分隔
