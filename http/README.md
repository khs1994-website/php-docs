---
title: HTTP 协议
date: 2013-02-01 13:00:00
updated:
comments: true
tags:
- HTTP
categories:
- HTTP
---

`HTTP` 属于应用层协议，在传输层使用 `TCP` 协议，在网络层使用 `IP` 协议。

* 无状态：无状态是指协议对于事务处理没有记忆能力。

* 无连接：限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。

* 面向连接

<!--more-->

# 头部属性

Accept	指定客户端能够接收的内容类型	Accept: text/plain, text/html

Accept-Charset	浏览器可以接受的字符编码集。	Accept-Charset: iso-8859-5

Accept-Encoding	指定浏览器可以支持的web服务器返回内容压缩编码类型。	Accept-Encoding: compress, gzip

Accept-Language	浏览器可接受的语言	Accept-Language: en,zh

Accept-Ranges	可以请求网页实体的一个或者多个子范围字段	Accept-Ranges: bytes

Authorization	HTTP授权的授权证书	Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

Cache-Control	指定请求和响应遵循的缓存机制	Cache-Control: no-cache

Connection	表示是否需要持久连接。（HTTP 1.1默认进行持久连接）	Connection: close

Cookie	HTTP请求发送时，会把保存在该请求域名下的所有cookie值一起发送给web服务器。	Cookie: $Version=1; Skin=new;

Content-Length	请求的内容长度	Content-Length: 348

Content-Type	请求的与实体对应的MIME信息	Content-Type: application/x-www-form-urlencoded

Date	请求发送的日期和时间	Date: Tue, 15 Nov 2010 08:12:31 GMT

Expect	请求的特定的服务器行为	Expect: 100-continue

From	发出请求的用户的Email	From: user@email.com

Host	指定请求的服务器的域名和端口号	Host: www.zcmhi.com

If-Match	只有请求内容与实体相匹配才有效	If-Match: “737060cd8c284d8af7ad3082f209582d”

If-Modified-Since	如果请求的部分在指定时间之后被修改则请求成功，未被修改则返回304代码

If-Modified-Since: Sat, 29 Oct 2010 19:43:31 GMT

If-None-Match	如果内容未改变返回304代码，参数为服务器先前发送的Etag，与服务器回应的Etag比较判断是否改变	If-None-Match: “737060cd8c284d8af7ad3082f209582d”

If-Range	如果实体未改变，服务器发送客户端丢失的部分，否则发送整个实体。参数也为Etag	If-Range: “737060cd8c284d8af7ad3082f209582d”

If-Unmodified-Since	只在实体在指定时间之后未被修改才请求成功	If-Unmodified-Since: Sat, 29 Oct 2010 19:43:31 GMT

Max-Forwards	限制信息通过代理和网关传送的时间	Max-Forwards: 10

Pragma	用来包含实现特定的指令	Pragma: no-cache

Proxy-Authorization	连接到代理的授权证书	Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

Range	只请求实体的一部分，指定范围	Range: bytes=500-999

Referer	先前网页的地址，当前请求网页紧随其后,即来路	Referer: http://www.zcmhi.com/archives/71.html

TE	客户端愿意接受的传输编码，并通知服务器接受接受尾加头信息	TE: trailers,deflate;q=0.5

Upgrade	向服务器指定某种传输协议以便服务器进行转换（如果支持）	Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11

User-Agent	User-Agent的内容包含发出请求的用户信息	User-Agent: Mozilla/5.0 (Linux; X11)

Via	通知中间网关或代理服务器地址，通信协议	Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)

Warning	关于消息实体的警告信息	Warn: 199 Miscellaneous warning

# 请求、响应消息组成 四部分

* 请求行（状态行）`HTTP 协议版本号 状态码 状态消息`

* 请求头部（消息报头）

* 空行

* 请求数据（响应正文）

```bash
HTTP/1.1 200 OK
Date: Fri, 22 May 2018 06:07:08 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive

请求数据（相应正文）
```

# url

协议 域名 端口 虚拟目录 文件名 锚（#XXX）参数（?xxx=xxx）

# 方法

* `get` `post` `head`

* `delete`

* `put` `patch`

* `options`

# 状态码

# 地址栏键入网址回车之后的过程

1. DNS 网址->IP

2. 通过 `IP + 端口` 和服务器建立 TCP 连接

3. 浏览器发出读取文件的 HTTP 请求，该请求报文作为 TCP 三次握手的第三个报文的数据发送给服务器

4. 服务器做出响应，把相应的 html 文件发给浏览器

5. 释放 TCP 连接

6. 浏览器解析 HTML，显示内容。

# IP

IP 协议主要解决网络路由和寻址问题。

# TCP 三次握手与四次挥手 控制传输协议

TCP 协议主要解决如何在 IP 层之上可靠地传递数据包，使得网络上接收端收到发送端所发出的所有包，并且顺序与发送顺序一致。

* 可靠的

* 面向连接的

# UDP 用户数据报协议

# 长连接 短链接

* HTTP/1.0 中默认使用短连接。每遇到这样一个 Web 资源，浏览器就会重新建立一个 HTTP 会话

* HTTP/1.1 起，默认使用长连接，用以保持连接特性。Keep-Alive 不会永久保持连接，它有一个保持时间，在 WEB 服务器中进行设定。
