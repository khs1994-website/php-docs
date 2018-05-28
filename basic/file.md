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

# HTML 上传文件

```html
<form action="url" method="post" enctype="multipart/form-data">
  <input type="file" name="name" id='file' />
  <input type="submit" />
</form>
```

PHP 会将文件存到临时文件中，脚本结束就会销毁，所以必须存到另外的位置。

```php
$file = $_FILE('file');

// 文件名
$file['name'];

// 类型
$file['type'];

// 临时文件名
$file['tmp_name'];

// error
$file['error'];

// size
$file['size'];

// 保存文件
move_uploaded_file($_FILES['file']['tmp_name'], '/path/filename');
```

# 获取路径

* 执行命令所在路径 `getcwd()`

* 文件所在路径 `__FILE__`

* 文件所在目录路径 `__DIR__ `dirname(__FILE__)`

# 目录相关函数

```php
resource opendir( string $path [, resource $context ] )
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

# SPL

## `SplFileInfo`

```php
$file = SplFileInfo('file');

$file->getExtension();

$file->getRealPath();
```

## `SplFileObject`

```php
$file = new SplFileObject($file_name [, $open_mode, $use_include_path, $context])

$file->eof();

$file->fgets();
```

# 文件操作相关函数

* 更改权限

  `chgrp()` `chmod()` `chown()`

* 复制

  `copy()`

* 删除

  `unlink()` `unset()`

* 判断

  `is_dir()` `is_file()` `is_executable()` `is_link()`

# 读写文件

官方文档：http://php.net/manual/zh/function.file-get-contents.php

`file_get_contents($filePath)`

`file_put_contents($filePath, $content)` 可以通过设置第三个参数，将内容追加，而不是覆盖。

官方文档：http://php.net/manual/zh/function.stream-get-contents.php

`stream_get_contents($resource)` 读取资源流到一个字符串

`stream_context_create($array)` 创建资源流上下文，参数必须为 `关联数组`

官方文档：http://php.net/manual/zh/function.fopen.php

```php
$fh = fopen($filePath, $mode);

// 返回类型为资源

fgets($fh); // 读取一行

fread($fh, $length);

fwrite($fh, $string);

fclose($fh);

file($filePath);

// 返回结果为数组，一行一个值
```
