---
title: ThinkPHP 入门
date: 2017-06-01 12:00:00
updated:
comments: true
tags:
- PHP
- ThinkPHP
categories:
- PHP
- ThinkPHP
---

# 安装

## composer

```bash
composer create-project topthink/think tp5 --prefer-dist
```

<!--more-->

# 添加新的模块

应用根目录执行

```bash
$ php think build --module demo
```
# 视图

URL访问
http://domainName/index.php/模块/控制器/操作
