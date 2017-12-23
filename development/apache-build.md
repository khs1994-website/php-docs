---
title: Apache 编译
date: 2016-09-10 13:00:00
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

本文介绍了手动编译安装 Apache 的具体步骤。

<!--more-->

# yum 方式安装

```bash
$ yum install wget epel-release
$ wget https://centos7.iuscommunity.org/ius-release.rpm
$ rpm -Uvh ius-release*rpm
$ yum install httpd24u
```

# 编译安装

## 安装所需软件

```bash
$ yum install gcc gcc-c++ make uuid-devel libuuid-devel unzip -y
```

`apr` 中包含了一些通用的开发组件，包括 mmap，DSO 等等  

`apr-util` 该目录中也是包含了一些常用的开发组件。这些组件与 apr 目录下的相比，它们与 apache 的关系更加密切一些。比如存储段和存储段组，加密等等。

`apr-iconv` 包中的文件主要用于实现 iconv 编码。目前的大部分编码转换过程都是与本地编码相关的。在进行转换之前必须能够正确地设置本地编码。因此假如两个非本地编码 A 和 B 需要转换，则转换过程大致为 A->Local 以及 Local->B 或者 B->Local 以及 Local->A。    

## 安装 apr

```bash
$ wget http://mirrors.tuna.tsinghua.edu.cn/apache//apr/apr-1.5.2.tar.gz
$ tar zxvf apr-1.5.2.tar.gz
$ cd apr-1.5.2
$ ./configure --prefix=/usr/local/apr

#下同
$ make
$ make install

```

## 安装 apr-iconv

```bash
$ wget http://mirrors.tuna.tsinghua.edu.cn/apache//apr/apr-iconv-1.2.1.tar.gz
$ tar -zxvf apr-iconv-1.2.1.tar.gz
$ cd apr-iconv-1.2.1
$ ./configure --prefix=/usr/local/apr-iconv --with-apr=/usr/local/apr
```

## 安装 apr-util

```bash
$ wget http://mirrors.tuna.tsinghua.edu.cn/apache//apr/apr-util-1.5.4.tar.gz
$ tar zxvf apr-util-1.5.4.tar.gz
$ cd apr-util-1.5.4
$ ./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr \
    --with-apr-iconv=/usr/local/apr-iconv/bin/apriconv
```

## 安装 pcre

```bash
$ wget  http://120.52.73.44/nchc.dl.sourceforge.net/project/pcre/pcre/8.38/pcre-8.38.zip
$ unzip  -o pcre-8.38.zip
$ cd pcre-8.38
$ ./configure --prefix=/usr/local/pcre
```

## Apache

```bash
# 替换 url 为实际的下载地址

$ wget url

$ tar zxvf httpd-2.4.20.tar.gz

$ cd httpd-2.4.20

$ ./configure --prefix=/usr/local/apache  \
      --enable-defalte --enable-expires \
      --enable-headers --enable-modules=most \
      --enable-so --with-mpm=worker \
      --enable-rewrite --with-apr=/usr/local/apr \
      --with-apr-util=/usr/local/apr-util \
      --with-pcre=/usr/local/pcre
```

# systemd

`yum` 方式安装会生成 `httpd.service` 文件，编译安装使用 `apache.service`

新建 `/lib/systemd/system/apache.service` 文件。


```yaml
[Unit]
Description=The Apache HTTP Server
After=network.target remote-fs.target nss-lookup.target
Documentation=man:httpd(8)
Documentation=man:apachectl(8)

[Service]
Type=simple
ExecStart=/usr/local/apache/bin/httpd -DFOREGROUND
ExecReload=/usr/local/apache/bin/httpd -k graceful
ExecStop=/bin/kill -WINCH ${MAINPID}
# We want systemd to give httpd some time to finish gracefully, but still want
# it to kill httpd after TimeoutStopSec if something went wrong during the
# graceful stop. Normally, Systemd sends SIGTERM signal right after the
# ExecStop, which would kill httpd. We are sending useless SIGCONT here to give
# httpd time to finish.
KillSignal=SIGCONT
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```
