---
title: Let's Encrypt SSL 证书配置详解
date: 2016-09-20 13:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
- Nginx
- https
categories:
- PHP
- php-dev-env
- Nginx
---

官方网站：https://letsencrypt.org/

GitHub：https://github.com/letsencrypt

首先确保你的网站是可以访问的（ nginx 配置好80端口），申请证书时 `let's Encrypt` 会访问网站上的某一文件来确认网站归属（当然也可以通过 DNS 确认）。

<!--more-->

# 第三方小工具 `acme.sh`

GitHub: https://github.com/Neilpang/acme.sh

请仔细阅读 `README.md`

## 安装 `acme.sh`

```bash
$ git clone https://github.com/Neilpang/acme.sh.git
$ cd ./acme.sh
$ ./acme.sh --install

# 脚本会自动建立别名
# Installing alias to '/home/ubuntu/.profile'

# 文件位于 ~/.acme.sh/

```

## 生成

请使用绝对路径或将 `~/.acme.sh/` 加入 `PATH`

```bash
$ acme.sh  --issue  -d mydomain.com -d www.mydomain.com  \
    --webroot  /home/wwwroot/mydomain.com/

# ECC证书

$ acme.sh --issue -w /home/wwwroot/example.com \
    -d example.com -d www.example.com \
		--keylength ec-256
```

生成的文件位于`~/.acme.sh/域名/`

## 转移证书文件

nginx 使用如下命令

```bash
$ acme.sh --installcert -d login.khs1994.com \
    --key-file /data/etc/nginx/conf.d/lets-acme/login.khs1994.com.key \
    --fullchain-file /data/etc/nginx/conf.d/lets-acme/login.khs1994.com.cer \
		--ecc
```

apache 请查看项目文档

## 使用 DNS 验证网站所用权

上边使用的方法，必须得保证网站可访问。使用 DNS 验证，就比较简单

将 DNS 服务商的 API 设置为系统变量，然后执行相关命令，具体请查看文档。

文档：https://github.com/Neilpang/acme.sh/tree/master/dnsapi

# 官方工具（不建议使用）

会安装很多依赖软件。

```bash
$ git clone https://github.com/letsencrypt/letsencrypt
$ cd letsencrypt
$ ./letsencrypt-auto certonly --email 邮箱 \
    -d 域名 -d 域名 \
		--webroot -w 网站目录完整路径 \
		--agree-tos
```

生成的证书位于`/etc/letsencrypt/live/`

nginx 配置如下

```nginx
ssl_certificate /etc/letsencrypt/live/域名/fullchain.pem;    
ssl_certificate_key /etc/letsencrypt/live/域名/privkey.pem;
```

# 相关链接

* acme.sh Wiki: https://github.com/Neilpang/acme.sh/wiki/%E8%AF%B4%E6%98%8E
