---
title: PHP curl 详解
date: 2016-10-17T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
categories:
  - PHP
  - Basic
---

本文详细记录了 PHP 使用 `curl` 遇到的问题。

<!--more-->

# https

```php
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 1);

// 设置 CA 根证书路径

curl_setopt($ch, CURLOPT_CAINFO, $value);

// 检查证书域名

curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, $value);

// 设置私钥路径

curl_setopt($ch, CURLOPT_SSLKEY, $value);

// 设置公钥路径

curl_setopt($ch, CURLOPT_SSLCERT, $value);
```

# htpasswd

```php
curl_setopt($ch, CURLOPT_USERPWD, $user.':'.$password);
```

# 参考链接

* http://blog.csdn.net/linvo/article/details/8816079

* https://segmentfault.com/a/1190000006220620
