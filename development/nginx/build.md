---
title: NGINX 编译安装
date: 2016-09-15 13:00:00
updated:
comments: true
tags:
- NGINX
categories:
- PHP
- NGINX
---

本文介绍了手动编译安装 NGINX 的具体步骤。

<!--more-->

# 建立用户及用户组

```bash
$ groupadd -r nginx

$ useradd -r -g nginx -s /bin/false -M nginx
```

## Alpine 较特殊

```bash
$ addgroup -S nginx

$ adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx
```

* http://git.alpinelinux.org/cgit/aports/tree/main/apache2/apache2.pre-install?h=v3.3.2
* http://git.alpinelinux.org/cgit/aports/tree/main/lighttpd/lighttpd.pre-install?h=v3.3.2
* http://git.alpinelinux.org/cgit/aports/tree/main/nginx-initscripts/nginx-initscripts.pre-install?h=v3.3.2

# 安装依赖包

RedHat 系

```bash
$ yum install -y gcc gcc-c++ pcre-devel openssl-devel zlib-devel
```

Debian 系

```bash
$ sudo apt install gcc g++ libpcre3 libpcre3-dev libssl-dev zlib1g-dev zlib1g
```

# 编译

```bash
$ ./configure --prefix=/etc/nginx  \
      --sbin-path=/etc/nginx/sbin/nginx \
      --conf-path=/etc/nginx/nginx.conf \
      --user=nginx \
      --group=nginx \
      --with-http_ssl_module \
      --with-http_realip_module \
      --with-http_addition_module \
      --with-http_sub_module \
      --with-http_dav_module \
      --with-http_flv_module \
      --with-http_mp4_module \
      --with-http_gunzip_module \
      --with-http_gzip_static_module \
      --with-http_random_index_module \
      --with-http_secure_link_module \
      --with-http_stub_status_module \
      --with-http_auth_request_module \
      --with-threads \
      --with-stream \
      --with-stream_ssl_module \
      --with-http_slice_module \
      --with-mail \
      --with-mail_ssl_module \
      --with-file-aio \
      --with-http_v2_module
```

# 错误排查

## 错误1

checking for OS
Linux 3.10.0-327.36.1.el7.x86_64 x86_64
checking for C compiler ... not found
./configure: error: C compiler cc is not found

```bash
$ yum install -y gcc gcc-c++

$ sudo apt install gcc g++
```

## 错误2

./configure: error: the HTTP rewrite module requires the PCRE library.You can either disable the module by using --without-http_rewrite_moduleoption, or install the PCRE library into the system, or build the PCRE librarystatically from the source with nginx by using --with-pcre=option.

```bash
$ yum install pcre-devel

$ sudo apt install libpcre3 libpcre3-dev
```

## 错误3

./configure: error: SSL modules require the OpenSSL library.You can either do not enable the modules, or install the OpenSSL libraryinto the system, or build the OpenSSL library statically from the sourcewith nginx by using --with-openssl=option.

```bash
$ yum install openssl-devel

$ sudo apt install libssl-dev
```

## 错误4

./configure: error: the HTTP gzip module requires the zlib library.

```bash
$ yum install zlib-devel

$ sudo apt install zlib1g-dev zlib1g
```

# 安装

```bash
$ make

$ sudo make install
```

## 加入环境变量

编辑 `~/.bash_profile`

```bash
export PATH=/etc/nginx/sbin:$PATH
```

编辑 `/etc/sudoers`

>注意：必须编辑此文件，否则 sudo 会找不到命令。

```bash
Defaults	secure_path="/etc/nginx/sbin:..."
```

# systemd

在 `/etc/systemd/system/` 下增加 `nginx.service` 文件，以下路径根据实际自己修改。

```yaml
[Unit]
Description=nginx - high performance web server
Documentation=http://nginx.org/en/docs/
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/etc/nginx/run/nginx.pid
ExecStartPre=/etc/nginx/sbin/nginx -t -c /etc/nginx/nginx.conf
ExecStart=/etc/nginx/sbin/nginx -c /etc/nginx/nginx.conf
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

# 启动

```bash
$ sudo nginx -t

$ sudo nginx
```

# 相关链接

* http://bbs.qcloud.com/thread-10429-1-1.html
