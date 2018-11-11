---
title: NGINX 配置
date: 2016-09-16 13:00:00
updated:
comments: true
tags:
- PHP
- NGINX
categories:
- PHP
- NGINX
---

本文详细介绍了 NGINX 常用配置。

官方文档：https://www.nginx.com/resources/wiki/start/topics/examples/full/

HTTPS https://github.com/khs1994-website/https

<!--more-->

* 内置变量 https://github.com/khs1994-docker/lnmp/issues/447

* 中文文档 https://github.com/oopsguy/nginx-docs)

修改主配置文件 `/etc/nginx/nginx.conf`

```nginx

worker_processes  auto;

http {
  # 配置首页
  # 在 http 段配置好，就不用在 server 段里配置了

  index index.php index.htm index.html;

  # 引入子配置文件

  include /etc/nginx/conf.d/*.conf;
}
```

# 命令

```bash
# stop 是快速停止 nginx，可能并不保存相关信息，quit 是完整有序的停止 nginx 并保存相关信息
$ nginx -s stop

$ nginx -s quit

# 重新打开日志文件命令
$ nginx -s reopen

# 重新载入配置文件
$ nginx -s reload
```

# 超时设置

```nginx
# 配置段: http, server, location 参数是一个请求完成之后还要保持连接多久，不是请求时间多久，目的是保持长连接
keepalive_timeout 75s;

# 配置段: http, server, location 接收客户端 body 超时
client_body_timeout 20s;

# 配置段: http, server, location 接收客户端 header 超时
client_header_timeout 10s;

# 配置段: http, server, location 服务端向客户端传输数据的超时时间。
send_timeout 30s;

# nginx 与 upstream server 的连接超时时间
proxy_connect_timeout 60s;

# nginx 接收 upstream server 数据超时, 默认 60s
proxy_read_timeout 60s;

# nginx 发送数据至 upstream server 超时
proxy_send_timeout 60s;

# 设置了某一个 upstream 后端失败了指定次数（max_fails）后，该后端不可操作的时间，默认为10秒
proxy_upstream_fail_timeout 10s;

# fastcgi php-fpm 等配置下列选项，上边的无用

fastcgi_connect_timeout 300;
fastcgi_send_timeout 300;
fastcgi_read_timeout 300;
```

## PHP

```php
ini_set('max_execution_time', '0'); // set_time_limit(0);

print str_repeat(" ", 4096);  //先输出4096的字节，保证缓冲数据量

For ($j = 1; $j <= 1000000; $j++) {
    echo $j.'';
    ob_flush();
    flush();//这一部会使cache新增的内容被挤出去，显示到阅读器上
    sleep(1);//让程序“睡”一秒钟，会让你把效果看得更清楚
}
```

# PHP

```nginx
server{
  root           /var/www2/www;

  location ~ \.php$ {
      # fastcgi_pass   unix:/run/php-fpm.sock;
      #
      # socket 方式不建议使用，WSL 必须用该方式
      #

      fastcgi_pass    phpfpm:9000;
      fastcgi_index   index.php;

      # 包管理工具 apt yum 安装的 nginx 不包含 fastcgi.conf
      # 必须使用注释的配置
      # fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
      # include        fastcgi_params;

      include          fastcgi.conf;
  }
}
```

# default_server

```nginx
server {
    listen       80  default_server;
    server_name  oschina.net  www.oschina.net;
}       
```

listen 指令后面有一个参数 `default_server` ，这个参数是在 0.8.21 版本以后才有的，而之前是 default 指令。Nginx的虚拟主机是通过 HTTP 请求中的 Host 值来找到对应的虚拟主机配置，如果找不到，那 Nginx 就会将请求送到指定了 `default_server` 的节点来处理，如果没有指定为 `default_server` 的话，就跑到 localhost 的节点，如果没有 localhost 的节点，那只好 404 了。

# 目录浏览功能

Nginx 默认是不允许列出整个目录的。如需此功能，在配置文件中 server 或 location 段里添加上 `autoindex on;` 来启用目录浏览。

```nginx
autoindex on;

# 默认为on，显示出文件的确切大小，单位是bytes。改为off后，显示出文件的大概大小，单位是kB或者MB或者GB

autoindex_exact_size off;

# 默认为off，显示的文件时间为GMT时间。改为on后，显示的文件时间为服务器时间

autoindex_localtime on;
```

# 负载均衡

```nginx
upstream fzjh {
    server 111.206.227.118 weight=2;
    server 123.206.62.18;
}

server {
    listen 80;
    server_name f.khs1994.com;
    location / {
      proxy_pass http://fzjh;
    }
}
```

# alias

假设请求 `url` 为 `http://localhost/appImg/abc.jpg`

```nginx
server {
  location ^~ /appImg/ {
    root /home/nginx; # /home/nginx/appImg/abc.jpg 路径拼接到了一起
  }

  location ^~ /appImg/ {
    #
    # alias 只能用在 location 块中
    #

    alias /home/nginx/; # 路径后必须加上 / ，/home/nginx/abc.jpg 会丢弃 location 匹配到的路径
  }
}
```

# 相关链接

* http://blog.csdn.net/benbendy1984/article/details/6025663

* http://nginx.org/en/docs/http/ngx_http_autoindex_module.html
