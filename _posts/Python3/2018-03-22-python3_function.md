---
layout: post
title: python3 函数的参数
category: Python3
tags: Python3
keywords:
description:
---
## 函数中参数传递是传值还是传引用传递？
答案: 都不是，python中一切皆对象，函数参数是传对象，类似于赋值操作。

参考[Python 函数中，参数是传值，还是传引用？](https://foofish.net/python-function-args.html)

## 位置参数，默认参数

```
  def adder(x，y=1):
      return x + y
```

对于adder(x)函数，参数x就是一个位置参数，参数y就是一个默认参数。

> Note: 默认参数防坑：
```
  def add_end(L=[])
      L.append('END')
      return L
```

当使用默认参数调用时，第一次运行结果是对的，第二次运行时结果就错了。原因如下：
- L是一个变量，它指向可变对象[]，每次调用该函数，如果改变了L的内容，则下次调用时，默认参数的
内容也跟着变了。

*我们在编写程序时，如果可以设计一个不变对象，那就尽量设计成不变对象，如str,None就是不变对象。*

## 可变参数

```
  def calc(*numbers):
      sum = 0
      for n in numbers:
https://foofish.net/python-function-args.html
https://foofish.net/python-function-args.html
https://foofish.net/python-function-args.html
https://foofish.net/python-function-args.html
定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个*号。在函数内部，参数numbers接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数。

如果已经有一个list或者tuple，要调用一个可变参数怎么办呢？
```
  nums = [1, 2, 3]
  calc(*nums)
```
`*nums`表示把nums这个list的所有元素作为可变参数传进去。

## 关键字参数
可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。

 ```
  def person(name, age, **kw):
      print('name:', name, 'age:', age, 'other:', kw)
  extra = {'city': 'Beijing', 'job': 'Engineer'}
  person('Jack', 24, **extra)
 ```
输出：
`name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}`

`**extra`表示把`extra`这个dict的所有key-value用关键字参数传入到`**kw`参数，`kw`将获得一个dict，注意`kw`获得的dict是`extra`的一份拷贝，对`kw`的改动不会影响到函数外的`extra`。

## 命名关键字参数
对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。如果要限制关键字参数的名字，就可以用命名关键字参数。
```
  def person(name, age, *， city, job):
      print('name:', name, 'age:', age, 'city:', city, 'job': job)
  person('Jack', 24, city='Beijing', job='Engineer')
```

使用命名关键字参数时，要特别注意，如果没有可变参数，就必须加一个`*`作为特殊分隔符。如果缺少`*`，Pyhton解释器将无法识别位置参数和命名关键字参数。

## 参数组合
> 参数定义的顺序必须是: 必选参数、默认参数、可变参数、命名关键字参数和关键字参数。

## 小结
- 默认参数一定要用不可变对象，否则会有逻辑错误。
- `*args`是可变参数，args接收的是一个list或者tuple;
- `**kw`是关键字参数，kw接收的是一个dict。
- 可变参数既可以直接传入：`func(1, 2, 3)`，又可以先组装list或tuple，再通过`*args`传入：`func(*(1, 2, 3))`；
- 关键字参数既可以直接传入：`func(a=1, b=2)`，又可以先组装dict，再通过`**kw`传入：`func(**{'a': 1, 'b': 2})`。
- 命名的关键字参数是为了限制调用者可以传入的参数名，同时可以提供默认值。
- 定义命名的关键字参数在没有可变参数的情况下不要忘了写分隔符*，否则定义的将是位置参数。
