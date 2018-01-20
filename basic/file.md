---
title: PHP 文件相关函数
date: 2016-10-13 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

本文介绍了 PHP 文件的相关函数。本文只是部分列举，详情请查看官方文档。

官方文档：http://php.net/manual/zh/book.dir.php

官方文档：http://php.net/manual/zh/book.filesystem.php

<!--more-->

# 执行命令所在路径

```php
getcwd()
```

# 文件所在路径

```php
__FILE__
```

# 文件所在目录路径

## 新的

```php
__DIR__
```

## 旧的

```php
dirname(__FILE__)
```

# 目录相关函数

```php
resource opendir ( string $path [, resource $context ] )
```

打开一个目录句柄，可用于之后的 `closedir()` `readdir()` `rewinddir()`。

* `readdir()` 从目录句柄中读取条目。

* `chdir()` 改变目录

* `chroot()` 改变根目录

* `closedir()` 关闭目录句柄

* `dir()` 返回一个 `Directory` 类实例

```php
$d=dir($path);

$d->handle;

$entry=$d->read();

$d->close();
```

* `getcwd()` 取得当前工作目录

* `rewinddir()` 倒回目录句柄

* `scandir()` 列出指定路径中的文件和目录

```php
array scandir ( string $directory [, int $sorting_order [, resource $context ]] )
```

返回包含文件和目录的数组。

# 文件相关函数

## ch...

`chgrp()` `chmod()` `chown()`

## 复制

`copy()`

## 删除

`unlink()` `unset()`

## 判断

`is_dir()` `is_file()` `is_executable` `is_link()`
