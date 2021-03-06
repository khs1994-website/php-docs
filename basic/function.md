---
title: PHP 函数
date: 2016-10-08 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

PHP 函数简介。

<!--more-->

# 常用函数

* `sys_get_temp_dir()` 返回用于临时文件的目录

* `htmlspecialchars()` 将特殊字符转换为 HTML 实体

# 匿名函数

```php
$example=function ($arg){
  echo $arg;
};

$example(1);

# 使用 use 使用外部变量

$message='hello';

$example=function () use ($message){
  return $message;
}

$example();

# use 引用变量
# 略
```

把第一个参数作为回调函数调用。

* `call_user_func($callback,$parameter,$parameter2)`

* `call_user_func_array($callback,$array)`

# 类型约束

## 参数

匿名函数类型 `closure`。

## 返回值

```php
declare(strict_types=1);

class C {}

function getC(): C // 限定返回类型
{
    return new C;
}

var_dump(getC());

/**
* :void 表明函数不返回数据
*
* @since 7.1
*/
function fun1(): void
{
  return;
}
```

# 可变函数

将函数名赋值给变量，通过变量调用函数。

```php
function a()
{

}

$var='a';

$var();   // 调用函数 a
```

同理，也可以将类的方法赋值给变量，通过调用变量调用方法。

# 函数参数

## 可变参数

```php
function fun1(...$a)
{
  var_dump($a); // array
}

fun1(1, 2, 3, 4);
```
