---
title: RESTful API 设计详解
date: 2017-03-10 12:00:00
updated:
comments: true
tags:
- PHP
- RESTful
categories:
- PHP
- RESTful
---

`RESTful` 是一种软件架构风格，其面向资源。基于 HTTP 协议实现。

慕课网：http://www.imooc.com/learn/811

<!--more-->

# 设计概念和准则

* 所有事物都可以被抽象为资源。

* 每一个资源都有唯一的资源标识，对资源的操作不会改变这些标识。

* 所有操作都是无状态的。

# 请求方法

* `get` 获取 =》查(SELECT)

* `post` 附加新的资源 (新建) =》增 (CREATE)

* `put` 请求服务器存储一个资源，并用 REQUEST-URI 作为其标识 更新 =》改 (UPDATE) 改全部信息

* `patch` 在服务器更新资源（客户端提供改变的属性）更新 => 改 (UPDATE) 改部分信息

* `delete` 请求服务器删除 REQUEST-URI 所标识的资源 =》删 (DELETE)

* `head` 请求获取由 REQUEST-URI 所标识的资源的响应信息报头

* `options` 请求查询服务器的性能，或者查询与资源相关的选项与需求

# 常用状态码

* `200` OK

* `400` Bad Request 客户端请求有语法错误，不能被服务器理解

* `401` Unauthorized 服务器受到请求，但拒绝提供服务

* `404` Not Found

* `500` Internal Server Error 服务器不可预期的错误

* `503` Server Unavailable 服务器当前不能处理客户端的请求

# 设计要素

## 资源路径 URI

每个网址代表一种资源，网址中不能有动词，只能是名词，名词应该是复数

## HTTP 动词

`get、post, etc`

## 过滤信息

`url?offset=10` 指定返回记录的开始位置

`url?limit=10` 指定返回记录的数量

`url?page=2&per_page=100` 指定第几页，以及每页的记录数。

`url?sortby=name&order=asc` 指定返回结果按照哪个属性排序，以及排序顺序。

`url?animal_type_id=1` 指定筛选条件

## 状态码

## 错误处理

```json
{
  "error":"错误信息"
}
```

## 返回结果

# More Information

* http://www.ruanyifeng.com/blog/2011/09/restful.html

* http://www.ruanyifeng.com/blog/2014/05/restful_api.html

* https://www.zhihu.com/question/28557115
