---
title: PHP 字符串相关函数
date: 2016-10-6 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
- Types
---

本文列举了 PHP 字符串相关函数。

<!--more-->

# 替换

```php
mixed str_replace( mixed $search, mixed $replace , mixed $subject [, int &$count]);
```

`$count` 如果被指定，它的值将被设置为替换发生的次数。

上述函数区分大小写，`str_ireplace()` 不区分大小写。
