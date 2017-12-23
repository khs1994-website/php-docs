---
title: WSL 快速搭建 LNMP 环境
date: 2017-12-22 12:00:00
updated:
comments: true
tags:
- LNMP
categories:
- PHP
---

`Windows Subsystem for Linux`（简称 `WSL` ）是一个为在 Windows 10 上能够原生运行 Linux 二进制可执行文件（ELF 格式）的兼容层。

<!--more-->

如何启用 `WSL` 这里不再赘述，下方执行命令过程中出错，可以使用 `sudo` 再次尝试执行。

本文基于如下软件

* `WSL` Ubuntu 16.04.3

* `nginx` 1.13.7

* `PHP` 7.2.0

* `Mysql` 5.7.20

# nginx

编辑 `/etc/apt/sources.list.d/nginx.list` 文件。

```bash
deb http://nginx.org/packages/mainline/ubuntu/ xenial nginx
```

添加密钥

```bash
$ sudo apt-key adv --keyserver ha.pool.sks-keyservers.net --keyserver-options timeout=10 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
```

安装

```bash
$ sudo apt update

$ sudo apt install nginx

$ sudo nginx
```

打开 `127.0.0.1` 看到 nginx 默认页面。

# PHP

详细编译说明请查看：https://www.khs1994.com/php/development/php-build.html

这里简要说明一下。

## 安装依赖

```bash
$ sudo apt install autoconf \
                   dpkg-dev \
                   file \
                   libc6-dev \
                   make \
                   pkg-config \
                   re2c \
                   gcc g++ \
                   libedit-dev \
                   zlib1g-dev \
                   libxml2-dev \
                   libssl-dev \
                   libsqlite3-dev \
                   libfreetype6-dev \
                   libxslt1-dev \
                   libcurl4-gnutls-dev \
                   libpq-dev \
                   libmemcached-dev \
                   libzip-dev \
                   libpng-dev \
                   libjpeg-dev

                   # ubuntu 16.04 没有 libargon2-0 ，17.04 + 才有，php 7.2.0 新特性
                   # libargon2-0 \
```

## 下载并解压源码包

```bash
$ cd /usr/local
$ sudo chmod 777 src
$ cd src
$ wget -O php-7.2.0.tar.gz http://hk1.php.net/get/php-7.2.0.tar.gz/from/this/mirror
$ tar -zxvf php-7.2.0.tar.gz
$ cd php-7.2.0
```

## 编译

```bash
$ ./configure --prefix=/usr/local/php \
    --with-config-file-path=/usr/local/php/etc \
    --with-config-file-scan-dir=/usr/local/php/etc/conf.d \
    --disable-cgi \
    --enable-fpm \
    --with-fpm-user=www-data \
    --with-fpm-group=www-data \
    --enable-ftp \
    --with-curl \
    --with-gd \
    --with-gettext \
    --with-iconv-dir \
    --with-kerberos \
    --with-libedit \
    --with-openssl \
    --with-pcre-regex \
    --with-pdo-mysql \
    --with-pdo-pgsql \
    --with-xsl \
    --with-zlib \
    --with-mhash \
    --with-png-dir=/usr/lib \
    --with-jpeg-dir=/usr/lib\
    --with-freetype-dir=/usr/lib \
    --enable-mysqlnd \
    --enable-bcmath \
    --enable-libxml \
    --enable-inline-optimization \
    --enable-gd-native-ttf \
    --enable-gd-jis-conv \
    --enable-mbregex \
    --enable-mbstring \
    --enable-opcache \
    --enable-pcntl \
    --enable-shmop \
    --enable-soap \
    --enable-sockets \
    --enable-sysvsem \
    --enable-xml \
    --enable-zip \
    --enable-calendar \
    --enable-intl \
    --enable-exif

    # ubuntu 16.04 没有 libargon2-0 ，17.04 + 才有，php 7.2.0 新特性
    # --with-password-argon2 \
```

## 安装

```bash
$ make -j "$(nproc)"

$ sudo make install
```

## 设置环境变量

编辑 `~/.bash_profile`

```bash
export PATH=/usr/local/php/sbin:/usr/local/php/bin:$PATH
```

编辑 `/etc/sudoers`

```bash
Defaults	secure_path="/usr/local/php/bin:/usr/local/php/sbin:..."
```

## 升级 pecl

```bash
$ sudo pecl update-channels
```

## 启动

```bash
$ sudo php-fpm -t

$ sudo php-fpm -D | -F
```

# MySQL

使用 `Docker for Windows`

```bash
$ docker run -it -d --name wsl-lnmp-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mytest -e MYSQL_DATABASE=test --mount src=wsl-lnmp-mysql-data,target=/var/lib/mysql mysql
```
