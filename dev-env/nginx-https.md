---
title: Nginx HTTPS 配置
date: 2017-07-27 13:00:00
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

# 完整配置文件

请点击这里访问：https://github.com/khs1994/nginx/blob/master/nginx.conf

# HSTS

* HTTP严格传输安全（HTTP Strict transport security，HSTS），配置浏览器对整个域名空间使用HTTPS来加密

```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubdomains; preload";
```

<!--more-->

# HPKP

* 公钥固定（Public Key Pinning）是指一个证书链中必须包含一个白名单中的公钥，也就是说只有被列入白名单的证书签发机构（CA）才能为某个域名*.example.com签发证书，而不是你的浏览器中所存储的任何 CA 都可以为之签发。

```bash
# 将中级证书内容写入 `lets.pem`

$ openssl x509 -noout -in lets.pem  \
    -pubkey | openssl asn1parse -noout \
    -inform pem -out public.key

$ openssl dgst -sha256 -binary public.key | openssl enc -base64

# 或者从https://myssl.com 证书详情，查看Pin值
```

```bash
add_header Public-Key-Pins 'pin-sha256="IiSbZ4pMDEyXvtl7Lg8K3FNmJcTAhKUTrB2FQOaAO/s="; pin-sha256="YLh1dUR9y6Kja30RrAn7JKnbQG/uEtLMkBgFF2Fuihg="; max-age=31536000; includeSubDomains; report-uri="https:/dev.khs1994.com/hpkp"';
```


# 证书加密类型

`RSA`  
`ECC`

# SSL测试网站

https://myssl.com/  
https://httpsecurityreport.com/?report=www.khs1994.com  
https://www.ssllabs.com/ssltest/index.html  

# 相关链接

* HTTPS 配置生成工具：https://mozilla.github.io/server-side-tls/ssl-config-generator/  
* https://www.fujieace.com/jingyan/nginx/hsts-hpkp.html  
* https://linux.cn/article-5282-1.html  
* http://www.scalescale.com/tips/nginx/hsts-nginx/  
* https://imququ.com/post/ecc-certificate.html  
