---
title: PHP7 编译安装
date: 2016-09-21 14:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

本文介绍了手动编译安装 PHP 的具体步骤。

<!--more-->

Debian9 Ubuntu17.04 出现错误请详细查看后边说明(PHP 7.1.9不会报错了)。出现错误强烈建议使用 https://stackoverflow.com 进行搜索！

# macOS

```bash
$ brew tap homebrew/homebrew-php

$ brew install php71
```

# 安装依赖包

## RedHat

```bash
$ yum install gcc \
              gcc-c++ \
              libxml2 libxml2-devel \
              openssl openssl-devel \
              libcurl libcurl-devel \
              freetype freetype-devel \
              libjpeg libjpeg-devel \
              libpng libpng-devel \
              libxslt libxslt-devel \
              systemd-devel \
              libicu-devel \
              libedit-devel
```

## Debian

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

# 编译

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

若编译 `Apache` 模块请添加 `--with-apxs2=/usr/local/apache/bin/apxs` 参数。

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
$ make -j "$(nproc)"

$ sudo make install
```

## 加入环境变量

编辑 `~/.bash_profile`

```bash
export PATH=/usr/local/php/sbin:/usr/local/php/bin:$PATH
```

编辑 `/etc/sudoers`

>注意：必须编辑此文件，否则 sudo 会找不到命令。

```bash
Defaults	secure_path="/usr/local/php/bin:/usr/local/php/sbin:..."
```

## 升级 pecl

```bash
$ sudo pecl update-channels
```

## 用户组

PHP-FPM 系统默认用户与用户组

Debian：www-data

RedHat: apache

# 复制配置文件

将源文件中的 `php.ini-development` 复制到安装目录中的 `lib` 子目录 ，并改名为 `php.ini`。

在源文件夹中执行以下命令，复制 `systemd` 文件。

```bash
$ cp sapi/fpm/php-fpm.serviceq /usr/lib/systemd/system/
$ systemctl daemon-reload
```

将安装目录中的 `etc` 子目录中的 `php-fpm.conf.default` 复制为 `php-fpm.conf`。

将安装目录中的 `etc/php-fpm.d` 子目录中的 `www.conf.default` 复制为 `www.conf`。

# systemd

已经在上一步中配置，这里贴出文件内容，便于学习。

```yaml
# It's not recommended to modify this file in-place, because it
# will be overwritten during upgrades.  If you want to customize,
# the best way is to use the "systemctl edit" command.

[Unit]
Description=The PHP FastCGI Process Manager
After=network.target

[Service]
Type=notify
PIDFile=/usr/local/php/var/run/php-fpm.pid
ExecStart=/usr/local/php/sbin/php-fpm --nodaemonize --fpm-config /usr/local/php/etc/php-fpm.conf
ExecReload=/bin/kill -USR2 $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

# 启动

```bash
$ sudo php-fpm

# 或者使用 system

$ sudo systemctl daemon-reload

$ sudo systemctl start php-fpm

# 也可以设置开机自启动

$ sudo systemctl enable php-fpm
```

# More Information

* https://segmentfault.com/a/1190000005363212

* https://stackoverflow.com/questions/42300393/php-7-1-2-compilation-and-libcurl-error
