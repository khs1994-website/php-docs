---
title: Laravel Session Cookie
date: 2017-03-10 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

Laravel Session cookie 介绍。

<!--more-->

# Session

```php
Illuminate\Http\Request 实例

->session()->get(); // 获取

           ->put(); // 新增

           ->forget(); // 删除

           ->flush(); // 清空

           ->pull(); // 取值之后删除

           ->flash(); // 闪存

// 辅助函数

session();

// 辅助函数新增值

session(['key'=>1])
```

# Cookie

```php
Illuminate\Http\Request 实例

->cookie('key'); // 获取 cookie

// 辅助函数设置 cookie，生成的是 cookie 实例，之后附加到响应。

$a=cookie(); // 与 PHP 原生 setcookie() 参数一致

return response()->cookie($a);

// 响应时设置 cookie

return response()->cookie(
  'name', 1 , 100
);
```
