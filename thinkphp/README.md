---
title: ThinkPHP 5 入门
date: 2016-09-25 12:00:00
updated:
comments: true
tags:
- PHP
- ThinkPHP
categories:
- PHP
- ThinkPHP
---

本文介绍了 ThinkPHP 5 安装以及简单的使用方法。

<!--more-->

# 安装

## composer

```bash
$ composer create-project --prefer-dist topthink/think=5.1.* tp5
```

# 添加新的模块

应用根目录执行

```bash
$ php think build --module demo
```

# 视图

访问 http://domainName/index.php/模块/控制器/操作
