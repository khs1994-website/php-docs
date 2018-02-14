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

PHP 7 可以通过 `try_catch` 来捕获错误 `Error e` 和异常 `Exception e`。

官方文档：http://php.net/manual/en/class.exception.php

官方文档：http://php.net/manual/en/class.throwable.php

<!--more-->

# 错误

```php
try {
  new A;
} catch (\Error $e) {
  echo $e->getMessage(); // Class 'A' not found
}
```

# 异常

```php
try {
  throw new Exception('发生异常');
} catch (\Exception $e) {
  echo $e->getMessage(); // 发生异常
}
```

# 解读

`Error` 和 `Exception` 都实现了 `Throwable` 接口。

官方文档：http://php.net/manual/en/class.throwable.php （暂无中文翻译）

# 自定义异常类和错误类

示例：https://github.com/khs1994-php/qq-login/blob/master/src/QQLogin/QQError.php

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

```php
ini_set("display_errors",0);

ini_set("error_reporting",E_ALL);

ini_set("error_log","日志文件路径");

ini_set("log_errors",1);
```
