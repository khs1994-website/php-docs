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

<!--more-->

# 匿名函数

```php
$example=function ($arg){
  echo $arg;
};

$example(1);

# 使用 use 指定参数。使用的是已定义变量

$message='hello';

$example=function () use ($message){
  return $message;
}

$example();

# use 引用变量
# 略
```

# 类型约束

## 参数

匿名函数类型 `closure`。

## 返回值

```php
declare(strict_types=1);

class C {}

function getC(): C
{
    return new C;
}

var_dump(getC());
```

# 函数变量

将函数名赋值给变量，通过变量调用函数。

```php
function a()
{

}

$var='a';

$var();   // 调用函数 a
```

同理，也可以将类的方法赋值给变量，通过调用变量调用方法。
