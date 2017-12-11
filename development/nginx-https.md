---
title: Nginx HTTPS 配置
date: 2016-09-18 13:00:00
updated:
comments: true
tags:
- php-dev-env
- Nginx
- HTTPS
categories:
- PHP
- php-dev-env
- Nginx
---

本文详细介绍了 HTTPS 配置。

GitHub：https://github.com/khs1994-website/nginx-https

<!--more-->

# 完整配置文件

# HSTS

HTTP 严格传输安全（HTTP Strict transport security，HSTS），配置浏览器对整个域名空间使用 HTTPS 来加密

```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubdomains; preload";
```

# HPKP(废弃)

[谷歌浏览器开发团队宣布将停止支持 HPKP 公钥固定](https://www.landiannews.com/archives/41904.html)

# 证书加密类型

`RSA`  
`ECC`

# SSL 测试网站

https://myssl.com/  
https://httpsecurityreport.com/?report=www.khs1994.com  
https://www.ssllabs.com/ssltest/index.html  

# 相关链接

* [HTTPS 配置生成工具](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
* https://www.fujieace.com/jingyan/nginx/hsts-hpkp.html
* https://linux.cn/article-5282-1.html
* http://www.scalescale.com/tips/nginx/hsts-nginx/
* https://imququ.com/post/ecc-certificate.html
