---
title: PHP7 编译安装
date: 2017-07-26 14:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

Debian9 Ubuntu17.04 出现错误请详细查看后边说明(PHP 7.1.9不会报错了)。出现错误强烈建议使用 https://stackoverflow.com 进行搜索！

<!--more-->

# 安装依赖包

## RedHat

```bash
$ yum install gcc gcc-c++ libxml2 libxml2-devel openssl openssl-devel \
   libcurl libcurl-devel freetype freetype-devel libjpeg \
   libjpeg-devel libpng libpng-devel libxslt libxslt-devel
```

## Debian

```bash
$ sudo apt install gcc g++ libxml2-dev libssl-dev pkg-config \
    libfreetype6-dev libxslt1-dev libcurl4-gnutls-dev
```

# 编译

```bash
$ ./configure --prefix=/usr/local/php --with-curl \
    --with-apxs2=/usr/local/apache/bin/apxs \
    --with-freetype-dir --with-gd --with-gettext \
    --with-iconv-dir --with-kerberos --with-libdir=lib64 \
    --with-libxml-dir --with-openssl --with-pcre-regex \
    --with-pdo-mysql --with-xsl --with-zlib \
    --enable-fpm \
    --enable-bcmath --enable-libxml \
    --enable-inline-optimization \
    --enable-gd-native-ttf --enable-mbregex \
    --enable-mbstring --enable-opcache --enable-pcntl \
    --enable-shmop --enable-soap --enable-sockets \
    --enable-sysvsem --enable-xml --enable-zip

```

# 错误排查

configure: error: no acceptable C compiler found

```bash
$ yum install -y gcc gcc-c++
$ sudo apt install gcc g++
```

configure: error: xml2-config not found. Please check your libxml2 installation.

```bash
$ yum install libxml2 libxml2-devel
$ sudo apt install libxml2-dev
```

configure: error: Cannot find OpenSSL...

```bash
$ yum install openssl openssl-devel
$ sudo apt install libssl-dev
```

configure: error: png.h not found.  

```bash
$ yum install libcurl libcurl-devel
$ sudo apt install libcurl4-openssl-dev
```

configure: error: freetype-config not found.

```bash
$ yum install freetype freetype-devel libjpeg libjpeg-devel libpng libpng-devel
$ sudo apt install libfreetype6-dev
```

configure: error: xslt-config not found. Please reinstall the libxslt >= 1.1.0 distribution

```bash
$ yum install libxslt libxslt-devel
$ sudo apt install libxslt1-dev
```

## Debian9

具体查看参考链接2

```
checking for cURL in default path not found
configure: error: Please reinstall the libcurl distribution easy.h should be in /include/curl/
```

```bash
$ sudo apt install libcurl4-gnutls-dev
```

注意，目前安装该包不能解决问题！需要建立软链接！！

```bash
$ sudo ln -s /usr/include/x86_64-linux-gnu/curl /usr/local/include/
```

编译选项改为 `--with-curl=/usr/local`


# 安装

```bash
$ make
$ sudo mkdir -p /usr/local/php
$ sudo chown $USER /usr/local/php
$ sudo chgrp $USER /usr/local/php
$ make install
```

# 复制配置文件

将源文件中的 `php.ini-development` 复制到安装目录中的 `lib` 子目录 ，并改名为 php.ini。

将安装目录中的 `etc`子目录中的 `php-fpm.conf.default` 复制为 `php-fpm.conf`。

将 `php-fpm.d` 中的 `www.conf.default` 复制为 `www.conf`。

# Systemd 服务

用 `systemctl` 命令来管理 `PHP-FPM`。以下路径根据实际自己修改。  
  
修改 `/usr/local/php/etc/php-fpm.conf`

```
pid = /var/run/php-fpm.pid
```

```bash
$ vi /lib/systemd/system/php7-fpm.service

[Unit]
Description=The PHP FastCGI Process Manager
After=syslog.target network.target

[Service]
Type=forking
PIDFile=/var/run/php-fpm.pid
ExecStart=/usr/local/php/sbin/php-fpm --nodaemonize --fpm-config /usr/local/php/etc/php-fpm.conf
ExecReload=/bin/kill -USR2 $MAINPID
ExecStop=/bin/kill -SIGINT $MAINPID

[Install]
WantedBy=multi-user.target
```

# 相关链接

* http://bbs.qcloud.com/thread-9907-1-1.html  
* https://stackoverflow.com/questions/42300393/php-7-1-2-compilation-and-libcurl-error
