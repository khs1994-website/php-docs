---
title: Laravel 文件上传
date: 2017-03-04 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

`Laravel` 文件上传相关内容。

<!--more-->

```php
$request->file('photo'); // ->photo; 也可以直接通过文件名调用
        ->hasFile('photo'); // 请求是否包含某文件
        ->isValid(); // 验证文件是否有效
        ->path();      // 文件路径
        ->extension(); // 文件扩展名
        ->store('images'); // 目录名，文件名会自动生成
        ->storeAs('images', 'filename.jpg'); // 指定目录及文件名
```
