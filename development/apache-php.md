---
title: Apache PHP 配置
date: 2016-09-12 13:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
- Apache
categories:
- PHP
- php-dev-env
- Apache
---

本文简要介绍了 `Apache` 解析 `PHP` 文件。

<!--more-->

# PHP-FPM

```apacheconf
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so

AddType application/x-httpd-php  .php
AddType application/x-httpd-php-source  .phps

DirectoryIndex  index.php  index.html
```

# 模块方式

>该方式太老，不建议使用

`/usr/local/apache2/modules/` 有 `libphp7.so` 文件。

PHP7 编译安装时加上参数 `--with-apxs2=/usr/local/apache2/bin/apxs`

```apacheconf
LoadModule php7_module        modules/libphp7.so
AddType application/x-httpd-php .php
```

## 配置

在子配置文件中写入以下内容

```apacheconf
<VirtualHost *:80>
    DocumentRoot "/var/www/htdocs"
    ServerName b.org
    ServerAlias www.b.org
    ErrorLog "logs/b.org.err"
    CustomLog "logs/b.org.access" combined
    <FilesMatch \.php$>
        SetHandler "proxy:fcgi://127.0.0.1:9000"
    </FilesMatch>

    <Directory "/app/test" >
      Options Indexes FollowSymLinks
      AllowOverride None
      Require all granted
    </Directory>    
</VirtualHost>
```
