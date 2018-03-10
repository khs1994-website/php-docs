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

>注意。PHP-FPM 暂时只能通过监听 socket ,不能设置 `listen 127.0.0.1:9000`！

GitHub：https://github.com/khs1994/wsl-php

<!--more-->

# 修订记录

* PHP-FPM 与 NGINX 只能通过 `socket` 方式连接，之前页面打开太慢解决不了，查看 GitHub 解决了该问题。

* 解决办法：https://github.com/Microsoft/WSL/issues/2100

# 安装

如何启用 `WSL` 这里不再赘述，下方执行命令过程中出错，可以使用 `sudo` 再次尝试执行。

# 软件列表

基于如下软件

* `WSL` Ubuntu 16.04.3

* `nginx` 1.13.9

* `PHP` 7.2.3

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

## 新增配置文件

apt 安装的 nginx 没有 `fastcgi.conf` 配置文件，我们必须手动加入

```bash
$ cd /etc/nginx

$ wget https://raw.githubusercontent.com/khs1994-docker/lnmp/master/config/etc/nginx/fastcgi.conf
```

## 修改主配置文件

https://github.com/Microsoft/WSL/issues/2100

解决 `PHP` 页面打开缓慢

```bash
$ sudo vi /etc/nginx/nginx.conf

http {
  ...

  fastcgi_buffering off; # 新加入此项

  ...
}
```

# PHP

详细编译说明请查看：https://www.khs1994.com/php/development/php-build.html

这里简要说明一下。

## 安装依赖

```bash
$ cd /usr/local

$ chown khs1994:khs1994 src  # 替换为自己的用户名

$ cd src

$ wget http://cn2.php.net/distributions/php-7.2.3.tar.gz

$ tar -zxvf php-7.2.3.tar.gz

$ cd php-7.2.3

$ sudo apt install autoconf \
                   dpkg-dev \
                   file \
                   ca-certificates \
                   curl \
                   xz-utils \
                   libc6-dev \
                   make \
                   pkg-config \
                   re2c \
                   gcc g++ \
                   libedit-dev \
                   libsodium-dev \
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

## 编译

```bash
$ ./configure --prefix=/usr/local/php \
    --with-config-file-path=/usr/local/php/etc \
    --with-config-file-scan-dir=/usr/local/php/etc/conf.d \
    --disable-cgi \
    --enable-fpm \
    --with-fpm-user=nginx \
    --with-fpm-group=nginx \
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
    --enable-exif \
    --with-sodium \
    --with-libzip

    #
    # --enable-gd-native-ttf 7.2.0 remove
    #
    # --with-libzip 7.2.0 add
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

$ pecl config-set php_ini /usr/local/php/etc/php.ini
```

## 配置

将源文件中的 `php.ini-development` 复制到安装目录中的 `etc` 子目录 ，并改名为 `php.ini`。

将安装目录中的 `etc` 子目录中的 `php-fpm.conf.default` 复制为 `php-fpm.conf`。

将安装目录中的 `etc/php-fpm.d` 子目录中的 `www.conf.default` 复制为 `www.conf`。

>非常重要！

新建 `/usr/local/php/etc/php-fpm.d/zz-wsl.conf` 文件

```bash
[global]

error_log = /var/log/php-fpm/error.log

[www]

access.log = /var/log/php-fpm/access.log

;
; 务必与 nginx 用户名一致
;

user = nginx
group = nginx

request_slowlog_timeout = 5
slowlog = /var/log/php-fpm/slow.log

listen = /run/php-fpm.sock

;
; 务必与 nginx 用户名一致
;

listen.owner = nginx
listen.group = nginx
listen.mode = 0660

env[APP_ENV] = wsl
```

## 启动

```bash
$ sudo php-fpm -t

$ sudo php-fpm -D | -F
```

# MySQL

## 使用 `Docker for Windows`

```bash
$ docker run -it -d --name wsl-lnmp-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mytest -e MYSQL_DATABASE=test --mount src=wsl-lnmp-mysql-data,target=/var/lib/mysql mysql
```

## 使用 WSL

```bash
$ sudo apt install mysql-server
```

# nginx 配置

编辑 `/etc/nginx/conf.d/php.conf`

```nginx
server {
  server_name 127.0.0.1;
  listen 80;
  root /app/test;
  index index.html index.php;
  location / {
    try_files $uri $uri/ /index.php?$query_string;
  }
  location ~ .*\.php(\/.*)*$ {
    # fastcgi_pass  127.0.0.1:9000;
    #
    # WSL 中请勿使用该配置
    #

    fastcgi_pass   unix:/run/php-fpm.sock;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
  }
}
```

# 尝试通过 pecl 安装 PHP 扩展

执行过程中若提示错误，请使用 `sudo`

```bash
$ sudo pecl update-channels

$ sudo pecl install redis memcached ...
```

编辑配置文件 `/usr/local/php/etc/php.ini` 在其最后添加

> 温馨提示：shift+g 即可在 vim 中跳到行尾。

```bash
extension=redis.so

extension=memcached
```

> 配置文件中不加扩展的后缀名也可以
