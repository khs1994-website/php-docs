---
title: PHP JSON XML 相关函数
date: 2016-10-15 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

本文介绍了 JSON 与 XML 相关函数。

<!--more-->

# JSON

## `json_encode()`

>将 `数组` 编码为 `json`

```php
json_encode($value [, $options, $depth]);
```

### `$options`

中文 `JSON_UNESCAPED_UNICODE` 以字面编码多字节 Unicode 字符（默认是编码成 `\uXXXX`）

## `json_decode()`

>将 json 解码为数组

```php
json_decode($json [, $assoc, $depth, $options]);
```

# XML
