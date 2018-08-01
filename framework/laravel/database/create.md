---
title: Laravel 创建数据库
date: 2017-03-06 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
- MySQL
categories:
- PHP
- Framework
- Laravel
---

使用数据库迁移创建数据库。

<!--more-->

```bash
$ php artisan make:migration create_name_table
```

新的迁移文件会被放置在 `database/migrations` 目录中。

在 `up` 方法中修改表结构。

迁移命令

```bash
$ php artisan migrate
```

回滚迁移

```bash
$ php artisan migrate:rollback
```
