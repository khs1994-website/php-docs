---
title: PHP 错误和异常处理
date: 2016-10-19 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

PHP 7 可以通过 `try_catch` 来捕获错误 `Error` 和异常 `Exception`。

官方文档：http://php.net/manual/en/class.exception.php

官方文档：http://php.net/manual/en/class.throwable.php

<!--more-->

# ini 设置

生产环境中不启用错误显示。

## 打开错误报告

### php.ini

```yaml
error_reporting = E_ALL # 错误报告级别

display_errors = On     # 是否显示错误

log_errors = On         # 是否记录日志

error_log = /var/log/php-fpm/php/error.log
```

### 脚本中设置

* http://php.net/manual/en/errorfunc.constants.php

```php
ini_set("display_errors",'On');

ini_set("error_reporting" ,'32767'); # php5.3 30719 php5.2 6143 previousliy 2047

ini_set("error_log", "日志文件路径");

ini_set("log_errors", 'on');
```

### 错误报告级别

* http://php.net/manual/en/class.throwable.php

* `E_[ALL | ERROR | WARNING | PARSE | NOTICE | STRICT | RECOVERABLE_ERROR | E_DEPRECATED]`

* `E_CORE_[ERROR | WARNING]`

* `E_COMPILE_[ERROR | WARNING]`

* `E_USER_[ERROR | WARNING | NOTICE | DEPRECATED]`

# 错误与异常捕获

可以像捕获异常那样来捕获错误。

```php
try {
  new A;
} catch (\Error $e) {
  echo $e->getMessage(); // Class 'A' not found
}

try {
  throw new Exception('发生异常');
} catch (\Exception $e) {
  echo $e->getMessage();
  // 发生异常
}

/*
* 一个 catch 使用管道（|）捕获多个错误或异常。
*
* @since 7.1
*/


try{

}catch (MyException | MyOtherException $e){

}

```

## 错误与异常种类

* https://segmentfault.com/a/1190000004219265#articleHeader0

* https://github.com/khs1994-php/error

`Error` 和 `Exception` 都实现了 `Throwable` 接口。

* `ArithmeticError` 算术运算错误

    * `DivisionByZeroError` 除数为 0 时错误

* `AssertionError` 断言错误

* `ParseError` 语法错误

* `TypeError` 函数类型错误（1.参数类型约束；2.返回值类型约束；3.参数个数少于函数参数）

    * `ArgumentCountError` 参数错误，函数传入参数个数少于函数参数。

# 自定义异常类和错误类

* https://github.com/khs1994-php/qq-login/blob/master/src/QQLogin/Error/QQError.php
