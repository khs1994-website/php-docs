---
title: PHPUnit Mock 测试
date: 2016-12-21 12:00:00
updated:
comments: true
tags:
- PHP
- PHPUnit
categories:
- PHP
- PHPUnit
---

本文介绍了 PHPUnit Mock 测试。

<!--more-->

假设 `foo` 函数调用了 `bar` 函数，那么在对 `foo` 函数进行单元测试会有两个问题：

foo 函数依赖于 bar 函数的结果，那么在对 foo 进行单元测试的时候必然会引入 bar ，那么这样子单元测试就没意义了，如果测试不通过，那么无法保证 bug 出在 foo 还是 bar。

bar 函数可能在测试环境不可执行，那么 foo 无法获取 bar 的执行结果，从而无法对 foo 进行单元测试。

Mock 测试就是为了解决上面的问题而出现的，使用 Mock 我们可以虚拟出一个 bar 的调用，并且假设 bar 调用返回结果。如果还是听不懂，上一段代码就知道了。

```php
class MockTest extends \PHPUnit\Framework\TestCase {
	public function testGet()
	{  
		$stub = $this->createMock(\App\UserService::class);     //1
		$stub->method('get')->willReturn(3); 					//2
		$this->assertEquals(3,$stub->get(1));  					//3
	}
}
```

上面的测试函数就使用到了 Mock，一行一行代码来分析：

第一行创建了一个虚拟的 UserService 对象。

第二行假设 UserService 中的 get 函数的返回值为 3。

第三行调用 $stub->get(1) 不会真的去执行 get 函数，而是根据第二行的 willReturn 函数直接返回 3。

# 参考链接

* https://juejin.im/post/5a40a3d551882506e50cdf70
