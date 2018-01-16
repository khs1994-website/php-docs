---
title: PHP 日期相关函数
date: 2016-10-16T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
categories:
  - PHP
  - Basic
---

# 设置时区

```php
date_default_timezone_get();

date_default_timezone_set('PRC');
```

<!-- more -->

# 时间戳

```php
time();
```

得到指定时间的时间戳

```php
mktime( [$hour, $min, $sec, $mon, $day, $year]);
```

将英文文本的日期或时间转换成时间戳

```php
strtotime($time [, $now]);

strtotime('+1 day');
```

微秒

```php
microtime( [$get_as_float]);

microtime(true);
```

# 输出时间

```php
date($format [, $timestamp]);

date('Y/m/d H:i:s');
```

# 其他

* `getdate()` 返回包含日期时间的数组

* `gettimeofday()` 返回包含时间信息的数组

* `checkdate()` 验证时间是否合法
