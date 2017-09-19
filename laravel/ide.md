---
title: laravel 框架 IDE 配置实现智能提示
date: 2017-07-22 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

# 配置composer

设置中搜索`composer`进行设置

# 安装 laravel-ide-helper

GitHub地址：https://github.com/barryvdh/laravel-ide-helper

<!--more-->

```bash
$ composer require barryvdh/laravel-ide-helper
```

`config/app.php`中`providers`中添加以下内容

```bash
Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```

通过命令行生成 `_ide_helper.php` 文件

```bash
$ php artisan ide-helper:generate
```

# 插件

`Laravel Plugin`
