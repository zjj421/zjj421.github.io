---
layout: post
title: Python Data Structures
category: Python3
tags: Python3
keywords:
description:
---
# Data Structures

## List

* Sequence Type
* listname = ["a", "b", "c"]
* 列表是有序的，可存储不同的数据类型，但常用做法是存储相同类型的数据。
* 列表是可迭代的（iterable），即可通过下标获取元素。如: list[0] = "a"
* 列表有下列方法：
  * list.append(x):　在list最后加上元素x。等价于: a[len(a):] = [x]
  * list.extend(iterable): 在list最后加上一组可迭代的元素。等价于: a[len(a):] = iterable
  * list.insert(i, x): 在list下标为i的元素前插入新的元素x。
  * list.remove(x): 移除list中值为x的第一个元素。如果么有该值，则会报错。
  * list.pop([i]): 移除list中下标为i的元素并返回该元素。如果省略i，则移除list中最后一个元素并返回该元素。
  * list.clear(): 移除list中所有元素。等价于: del a[:]
  * list.index(x[, start[, end]]): 返回list中第一个值为x的元素的下标。可选参数start和end为搜索范围，所有下标都是从０开始的。
  * list.count(x): 返回list中值为x的元素的个数。
  * list.sort(key=None, reverse=False): 给list中的元素按其unicode编码值排序，默认为升序。如果list中保存的不是同一类型的，则会报错。该sort()方法直接修改list，而内置函数sorted()返回一个新的排序好的list,原list并不会被改变。
  * list.reverse(): 倒转该list中的元素。
  * list.copy(): 返回一个**新的**list。(Return a **shallow copy** of the list.)　等价于: a[:]
    * 示例：
    ```
      a = [1, 2, 3]
      b = [4, 5 6]
      c = a
      c.extend(b)  # 此时 c = [1, 2, 3, 4, 5, 6], a = [1, 2, 3, 4, 5, 6]
    ```
    * 如果上面 c = a 改为 c = a.copy() 或者 a[:], 则 c 和 a 是独立的２个变量。
* 实例：
  ```
  >>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
  >>> fruits.count('apple')
  2
  >>> fruits.count('tangerine')
  0
  >>> fruits.index('banana')
  3
  >>> fruits.index('banana', 4)  # Find next banana starting a position 4
  6
  >>> fruits.reverse()
  >>> fruits
  ['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
  >>> fruits.append('grape')
  >>> fruits
  ['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
  >>> fruits.sort()
  >>> fruits
  ['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
  >>> fruits.pop()
  'pear'
  ```
* list可以在堆栈中使用：
  * list.apend(): 先进
  * list.pop(): 后出
* list同样可在队列中使用,不过在list的最前面删除元素开销比较大。因为list是线性序列，在其最后面添加或删除元素特别快。我们可以利用collection模块中的deque函数来实现队列：
  ```
  from collection import deque
  queue = queue(listname)
  queue.apend("anotheritem")
  queue.popleft() # 先出
  ```

## tuple

* Sequence Type
* tuplename = (1248,8421,"Hello")
* 元组是无序的，是不可变对象，其值初始化后不能更改。但是其可以包含不可变对象，比如list,因为tuple保存的是list的name,list中元素变动，其name并不会改变。
* tuple由许多由逗号分割开的值组成，一般用圆括号括起来。注意包含0个或一个元素的tuple，空tuple用圆括号括起来，只含一个元素的tuple在元素后面加一个逗号。
  * empty = ()
  * singleton = ("Hello",)　　一般用括号括起来。
