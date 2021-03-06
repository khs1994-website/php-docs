---
title: PHP PDO MySQL
date: 2017-04-02 13:00:00
updated:
comments: true
tags:
- PHP
- PDO
- MySQL
categories:
- PHP
- PDO
- MySQL
---

# 连接

<!--more-->

```php
// 数据源

$dsn='mysql:host=localhost;dbname=imooc;port=3306';

// uri 形式

$dsn='uri:file://G:\path'

$pdo=new PDO($dsn,$username,$password);

var_dump($pdo);
```

# `exec()`

>执行一条 `SQL` 语句，并返回其受影响的行数。

* 对于 `select` 没有作用。

* 可用于 `创建表 数据库` `插入记录` `更新` `删除`

```php
$query=<<<EOF
  CREATE TABLE IF NOT EXISTS tablename(...)
EOF;

$res=$pdo->exec($query);

// 最后插入记录的 ID 号

$id=$pdo->lastInsertId();

var_dump($res);

var_dump($id);

// 获取错误信息

$pdo->errorCode(); // string

$pdo->errorInfo(); // array

// 使用 try-catch 捕获 PDOException

```

# `query()`

> 查询，执行一条 `SQL` 语句，返回一个 `PDOStatement` 对象

* `查询` `插入`

```php
$sql='select * from tablename';

$stmt=$pdo->query($sql);

// 之后通过遍历数组，获取结果
```

# `prepare()` `PDOStatement::execute()`

* `prepare()` 准备要执行的 `SQL` 语句，返回 `PDOStatement` 对象

* `PDOStatement::execute()` 通过调用该方法处理预处理过的语句

```php
$stmt=$pdo->prepare($sql);

$stmt->execute(); // 返回布尔类型

$stmt->fetch(); // 默认返回关联 + 索引数组，得到结果集中一条记录

// 可以在 fetch 时设置返回形式，只返回关联数组，失败返回 false

$stmt->fetchAll(PDO::FETCH_ASSOC); //  PDO::FETCH_NUM PDO::FETCH_BOTH

// 也可以先设置返回形式，再 fetch。和上一种方法二选一

$stmt->setFetchMode(PDO::FETCH_ASSOC);

$stmt->fetchAll(); // 二维数组，返回所有数据，失败返回 false
```

# `setAttribute()` `getAttribute()`

>设置，得到数据库连接属性

```php
$pdo->getAttribute($attribute);

$pdo->setAttribute($attribute, $value);

// PDO::ATTR_ERRMODE PDO::ERRMODE_EXCEPTION | ERRMODE_SILENT(default) | ERRMODE_WARNING
```

# `quote()`

>返回带引号的字符串，防止 SQL 注入

```php
$pdo->quote($usernmae);
```

# `rowCount()`

* `select` 操作，返回结果集中记录的条数

* `insert` `update` `delete` 操作，返回受影响的记录的条数

```php
$stmt->rowCount();
```

# 预处理语句中的占位符

> 也可以防止 SQL 注入

```php
$sql='select * from tablename where username=:username';

// 通过 ? 占位

$sql='select * from tablename where username=?';

$stmt=$pdo->prepare($sql); // 返回 PDOStatement 对象

$stmt->execute([':username'=>$usernmae]); // 调用的是 PDOStatement 对象的 execute 方法

// ? 占位

$stmt=execute([$username]);
```

# 绑定参数到指定的变量

`bindParam()`

```php
// :var 占位
$username='usernmae';

$stmt->bindParam(':username',$username); // 第二个参数不能是具体的值，第二个参数是引用类型

$username='usernmae2'; // 实际值为 username2

$stmt->execute();

// ? 占位，索引从 1 开始

$stmt->bindParam(1,$username);

$stmt->execute();
```

# 把一个值绑定到参数

`bindValue()`

```php
$username='username';

// :var 占位

$stmt->bindValue(':var',$username); // 第二个参数可以是具体的值

$username='username2'; // 实际值为 username

// ? 占位

$stmt->bindValue(1,$username);
```

## 注意以上两者的区别

* 第二个参数是否为引用变量

# 绑定结果中的一列到一个 PHP 变量

`bindColumn()`

```php
$stmt->execute();

$stmt->bindColumn(1,$username);

while ($stmt->fetch(PDO::FETCH_BOUND)) {
  echo 'username:'.$username;
}
```

# 其他

* `columnCount()` 返回结果集的列数

* `getColumnMeta()` 返回结果集中一列的元数据，索引从 0 开始

* `fetchColumn()` 从结果集中返回一列，索引从 0 开始

* `debugDumpParams()` 打印预处理语句

* `nextRowset()` 将结果集中的指针下移
