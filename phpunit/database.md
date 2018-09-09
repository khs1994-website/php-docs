---
title: PHPUnit 数据库测试
date: 2016-12-22 12:00:00
updated:
comments: true
tags:
- PHP
- PHPUnit
categories:
- PHP
- PHPUnit
---

PHPUnit 数据库测试。

```bash
$ composer require --dev phpunit/dbunit
```

<!--more-->

```php
use PHPUnit\DbUnit\TestCaseTrait;

class TestExample extends TestCase
{
    use TestCaseTrait;

    // 设置数据库连接，必须实现
    public function getConnection()
    {
        // $pdo = new PDO();
        $pdo = DB::connection();

        return $this->createDefaultDBConnection($pdo, ':memory');
    }

    // 创建数据集，必须实现
    protected function getDataSet()
    {
        // return $this->createFlatXMLDataSet(__DIR__.'/db_flat.xml');

        // return $this->createXMLDataSet(__DIR__.'/db.xml');

        return $this->createArrayDataSet(
        [
            'builds' => [
                [
                    'id' => 1,
                ],
                [
                            'id' => 2,
                ],
            ],
        ]);
    }

    public function test(){
        $this->assertEquals(2, $this->getConnection()->getRowCount('builds'));
    }
}
```

# 参考链接

* https://segmentfault.com/a/1190000008953673
