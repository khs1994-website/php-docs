---
title: PHP 数组相关函数
date: 2016-10-7 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
- Types
---

本文列举了 PHP 数组相关函数。

<!--more-->

# 常用函数

* `count(mixed $var [, int $mode = COUNT_NORMAL])` 数组长度，也可以返回对象的属性个数

* `list($a, $b, $c) = [1, 2, 3]` `list('a' => $a) = ['a' => 1]` 把数组中的值赋给一组变量

* `array_filter($arg [, $callback, $use_keys])` 去掉数组中的空值

* `array_merge($arr1, $arrays...);`

# 字符串与数组转化

* `string implode( string $glue, array $array)` 一维数组转化为字符串

返回一个字符串，由 `$glue`（默认为空） 分隔开的数组的值。

* `array explode( string $delimiter , string $string [, int $limit])` 分隔字符串，返回数组

使用特定的分隔符 (`$delimiter`) 分隔字符串 (`$string`)，返回一个数组。

`$limit` 限制返回数组的元素个数，如果结果大于 `$limit`，则最后一个元素包含剩余的结果。

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

// 判断数组中是否存在指定的 key

bool array_key_exists('id', $name['desc']);

// 检查数组中是否存在某个值

bool in_array(23, $name['desc']);

// 搜索值，返回键名

var_dump(array_search(34,$name['desc']));
```

# 排序

```php
// 升序

sort(&$arg [, $sort_flags]);

// 降序

rsort(&$arg [, $sort_flags]);

// 按键排序

ksort(&$arg [, $sort_flags]);

krsort(&$arg [, $sort_flags]);

// 按值排序

asort(&$arg [, $sort_flags]);

arsort(&$arg [, $sort_flags]);
```
