---
title: PHPUnit 详解
date: 2016-12-20 12:00:00
updated:
comments: true
tags:
- PHP
- PHPUnit
categories:
- PHP
- PHPUnit
---

本文介绍了 `PHP` 单元测试框架 `PHPUnit`。

官方网站：https://phpunit.de/

GitHub：https://github.com/sebastianbergmann/phpunit

<!--more-->

# 安装

`composer` 引入，执行命令或直接编辑文件。

```bash
$ composer require --dev phpunit/phpunit
```

```json
{

"require-dev": {
        "phpunit/phpunit": "^6.2"
}

}
```

# 使用

```php
use PHPUnit\Framework\TestCase;

// 被测试的类加 Test

class ClassTest extends TestCase
{
  // test 加被测试的函数

  public function testFunction()
    // code
}
```

## 不用另外编写测试代码

```php
class Calculator  
{  
   /**
    * @assert (0, 0) == 0
    * @assert (0, 1) == 1
    * @assert (1, 0) == 1
    * @assert (1, 1) == 2
    */

    public function sum($a, $b)  
    {  
        return $a + $b;  
    }  
}  
```

```bash
$ phpunit --skeleton Calculator.php
```

# 示例

* https://github.com/khs1994-php/tencent-ai
