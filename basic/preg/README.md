---
title: PHP 正则表达式
date: 2017-05-01T12:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - Preg
categories:
  - PHP
  - Preg
---

本文主要介绍了 PHP 正则表达式相关的函数。

官方文档：http://php.net/manual/zh/ref.pcre.php

<!-- more -->

# 表单验证

```php
int preg_match($pattern, $subject, [ array &$matches ])

int preg_match_all($pattern, $subject, array &$matches)
```

返回匹配到结果的次数，结果放到第三个参数的数组中。

# 搜索替换 词语过滤

```php
preg_replace($pattern, $replacement, $subject)

preg_filter($pattern, $replacement, $subject) // 只保留发生替换的字符串
```

```php
preg_grep($pattern, array $input) // 阉割版 preg_filter，只返回匹配到的值
```

```php
preg_split($pattern, $subject) // 升级版的 explode
```

```php
preg_quote($str) // 转义
```

# 基本概念

* 界定符 `/正则表达式/`

* 原子

* 量词

* 边界控制

* 模式单元
