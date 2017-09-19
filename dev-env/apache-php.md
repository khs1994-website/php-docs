---
title: Apache PHP 配置
date: 2017-05-03 13:00:00
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

# 模块方式

`/usr/local/apache/modules/` 有`libphp7.so`文件

PHP7编译安装时加上参数 `--with-apxs2=/usr/local/apache/bin/apxs`

```apacheconf
LoadModule php7_module        modules/libphp7.so
AddType application/x-httpd-php .php
```

<!--more-->

# PHP-FPM

```apacheconf
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so

AddType application/x-httpd-php  .php
AddType application/x-httpd-php-source  .phps

DirectoryIndex  index.php  index.html
```

## 配置

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
</VirtualHost>
```
