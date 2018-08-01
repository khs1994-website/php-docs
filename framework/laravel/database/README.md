---
title: Laravel 数据库操作
date: 2017-03-06 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
- MySQL
categories:
- PHP
- Framework
- Laravel
---

可以使用 `原生 SQL` `查询构造器` `Eloquent ORM`。

<!--more-->

# 原生 SQL

同原始 `PDO` 一样支持两种绑定参数的方式。

## 插入 `insert`

使用 `?` 绑定参数

```php
DB::insert('insert tb1 values(?,?,?)',[null,'tom',10]);
```

> 返回布尔值

使用 `:var` 绑定参数

```php
DB::insert('insert tb1 values(:id,:username,:age)',[
    'id'=>null,
    'username'=>'tom',
    'age'=>10
]);
```

## 查询 `select`

```php
DB::select('select * from tb1 where id = :id',[
    'id'=>1
]);
```

> 返回一个数组结果集，数组中的每个结果将是一个 PHP `stdClass` 对象。

## 更新 `update`

```php
DB::update('update tb1 set name=? where id = ?',['khs1994',1]);
```

> 返回所影响的行数

## 删除 `delete`

```php
DB::delete('delete from tb1');
```

> 返回所影响的行数

## `statement`

> 适用于没有返回值的 SQL 语句。

```php
DB::statement('drop table tb1');
```

# 数据库请求构造器

## 获取所有数据列 `get`

```php
DB::table('tb1')->get();
```

>返回一个 `Illuminate\Support\Collection` 结果，其中每个结果都是一个 PHP `StdClass` 对象的实例

## 获取单列或单行

获取一行数据，使用 `first` 方法。

```php
DB::table('tb1')
  ->where('name','John')
  ->first();
```

取出一行中的单个值。

```php
DB::table('tb1')
  ->where('name','John')
  ->where('name','like','J%')
  ->where('age','=',10)
  ->value('age')
```

获取一列值。

```php
DB::table('tb1')
  ->pluck('title')
```

## 结果分块 `chunk`

```php
DB::table('tb1')->orderBy('id')->chunk(100,function($users){
  foreach ($users as $k){

  }
})
```

## 聚合函数

```php
DB::table('tb1')
    ->count()
    ->min('price')
    ->max('price')
    ->avg('price')
    ->sum('price')

```

## `select`

```php
DB::table('tb1')
    ->select('name','user_email as email')
    ->distinct() // 去掉重复结果
    ->get();
```

也可以在已有的查询构造器实例上调用 `addselect('age')`。
