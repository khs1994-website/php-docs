---
title: PHP 杂项记录
date: 2018-03-02 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
---

记录一些 PHP 知识。

<!--more-->

# 系统环境变量

`php.ini`

```bash
; http://php.net/manual/zh/ini.core.php#ini.variables-order

variables_order = "GPCS"
```

此时 `$_ENV` 数组为空，此时可以通过 `getenv('var')` 获取变量对应的值。当没有值传入时，返回包含全部系统变量的关联数组。

若设置为 `EGPCS` ，此时 `$_ENV` 包含有系统的环境变量。

# `eval()`

* `eval()` 把字符串作为 PHP 代码执行 `eval('echo 1;')`

# `fastcgi_finish_request()`

* PHP-FPM 结束网页请求，但后台 PHP 脚本仍然在执行。

# 纯 PHP 文件末尾不加 ?>

* https://github.com/khs1994-docker/lnmp/issues/578
