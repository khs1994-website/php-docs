---
title: PHP 数组相关函数
date: 2017-08-14 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
---

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

<!--more-->
