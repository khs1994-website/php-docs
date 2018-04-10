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

GitHub：https://github.com/khs1994-php/wsl

<!--more-->

# 修订记录

* PHP-FPM 与 NGINX 只能通过 `socket` 方式连接，之前页面打开太慢解决不了，查看 GitHub 解决了该问题。解决办法：https://github.com/Microsoft/WSL/issues/2100

* Windows 支持 Debian 9 我们可以在 Docker 中编译 PHP 之后将编译好的文件复制出来即可，本人目前采用此方法。

* 如何启用 `WSL` 这里不再赘述，下方执行命令过程中出错，可以使用 `sudo` 再次尝试执行。

# 软件列表

基于如下软件

* `WSL` Debian 9

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
$ curl -fsSL http://nginx.org/packages/keys/nginx_signing.key | sudo apt-key add -
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

$ sudo wget https://raw.githubusercontent.com/khs1994-docker/lnmp/master/config/etc/nginx/fastcgi.conf
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

详细编译说明请查看：https://www.khs1994.com/php/development/build.html

从 Docker 复制编译好的 PHP 请查看 GitHub，有疑问请提出 issue.

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

编辑配置文件 `/usr/local/php/etc/php.ini` 在文件开头添加

```bash
extension=redis

extension=memcached
```
