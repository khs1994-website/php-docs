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

```php
int preg_match($pattern, $subject, [ array &$matches ])

int preg_match_all($pattern, $subject, array &$matches)
```

返回匹配到结果的次数。

preg_replace($pattern, $replacement, $subject)

preg_filter($pattern, $replacement, $subject)

preg_grep($pattern, array $input)

preg_split($pattern, $subject)

preg_quote($str)
