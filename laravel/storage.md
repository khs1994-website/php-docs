---
title: Laravel 文件系统
date: 2017-03-06 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

Laravel 文件系统相关介绍。

<!--more-->

建立链接 `storage/app/public` -> `public/storage`

```bash
$ php artisan storage:link
```

```php
Storage::disk('local')->

// 默认路径为 storage/app

Srorage::put('public/1.txt',1);

// 生成文件访问链接

asset('storage/1.txt');

Storage::get('public/1.txt');

::exists('public/1.txt');

::url('public/1.txt');

```
