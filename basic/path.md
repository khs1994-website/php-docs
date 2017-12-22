---
title: PHP 路径相关函数
date: 2016-10-13 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
---

主要包括 `getcwd()` `__FILE__` `__DIR__`

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
