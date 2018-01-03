---
title: PHP 数组相关函数
date: 2016-10-10 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

本文列举了 PHP 数组相关函数。

<!--more-->

# 判断数组某一值是否存在

```php
$name = [
    "name" => "tom",
    "age=>12",
    'desc' =>
        [
            23,34,35
        ]
];

//判断某个数组中是否存在指定的 key

var_dump(array_key_exists('id', $name['desc']));

//搜索值

var_dump(in_array(23, $name['desc']));

//返回键名

var_dump(array_search(34,$name['desc']));
```

# 去掉数组中的空值

```php
array_filter($arg [, $callback, $use_keys]);
```

# 合并多个数组

```php
array_merge($arr1, $arrays...);
```

# 排序

```php
// 升序

sort(&$arg [, $sort_flags]);

// 降序

rsort(&$arg [, $sort_flags]);

// 按键排序

ksort(&$arg [, $sort_flags]);

// 按值排序

asort(&$arg [, $sort_flags]);

krsort(&$arg [, $sort_flags]);

arsort(&$arg [, $sort_flags]);
```
