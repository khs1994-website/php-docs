---
title: Nginx 编译安装
date: 2016-09-15 13:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
- Nginx
categories:
- PHP
- php-dev-env
- Nginx
---

本文介绍了手动编译安装 nginx 的具体步骤。

<!--more-->

# 安装依赖包

RedHat 系

```bash
$ yum install -y gcc gcc-c++ pcre-devel openssl-devel zlib-devel
```

Debian 系

```bash
$ sudo apt install libpcre3 libpcre3-dev libssl-dev zlib1g-dev zlib1g
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
$ sudo mkdir -p /etc/nginx
$ sudo chown $USER /etc/nginx
$ sudo chgrp $USER /etc/nginx
$ groupadd -r nginx \
  && useradd -r -g nginx -s /bin/false -M nginx

# 开始编译安装

$ make
$ make install
```

# 启动

将 `/etc/nginx/sbin` 加入 `PATH` 或者软链接到 `PATH` ,之后启动

```bash
$ sudo nginx -t
$ sudo nginx
```

# systemd

在 `/lib/systemd/system/` 下增加 `nginx.service` 文件，以下路径根据实际自己修改。

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

# 相关链接

* http://bbs.qcloud.com/thread-10429-1-1.html
