---
title: PHP OAuth2 详解
date: 2016-11-10 12:00:00
updated:
comments: true
tags:
- PHP
- OAuth2
categories:
- PHP
- OAuth2
---

开放式授权。

<!--more-->

这里以 QQ 代替 OAuth 服务器。

# 网站放置网址

# 用户点击

# 网站请求 QQ 登录页

`Request Token URL` 未授权的令牌请求服务地址: QQ 服务器地址+特定参数

* client_id （站点 ID）

* redirect_uri  (回调地址)

# 用户输入用户名、密码

# QQ 给网站返回结果

跳转到网站回调地址，带有特定参数

* code

网站获取 code 参数

网站再次向 QQ 发起请求

`User Authorization URL` 用户授权的令牌请求服务地址: QQ 服务器+特定参数

* client_id (站点 ID)

* client_secret (站点密钥)

* code （有有效期）

然后 QQ 服务器返回包含用户信息的结果，网站解析之后跳转页面

返回数据包含 `AccessToken` (有有效期)

# 网站跳转

# 获取信息

网站可以使用 `AccessToken` 从 QQ 获取用户的信息信息。

`RefreshToken` 刷新 `AccessToken`
