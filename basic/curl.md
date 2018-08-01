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

* http://php.net/manual/zh/book.curl.php

GitHub：https://github.com/khs1994-php/curl

<!--more-->

# Windows Curl SSL

https://curl.haxx.se/docs/caextract.html

点击最新的日期，下载文件放到 `c:\cacert-2018-03-07.pem`

`php.ini` 增加如下配置

```bash
curl.cainfo="c:\cacert-2018-03-07.pem"
```

# 初始化

```php
$ch=curl_init();
```

# 设置网址

```php
curl_setopt($ch, CURLOPT_URL, $url);
```

# post

```php
curl_setopt($ch, CURLOPT_POST, 1);

curl_setopt($ch, CURLOPT_POSTFIELDS, $data)
```

## post 表单

```php
$data=[
  $media=new CURLFile($filePath)
];

# 旧版本是 @加文件名，新版已废弃。

curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
```

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
