---
layout: post
title: C++ Data Structures
category: C++
tags: C++
keywords:
description:
---

参考自[这里](https://www.geeksforgeeks.org/c-data-types/)

### 数据类型

#### Primitive Data Types 内置数据类型

- Integer 整型
```
Keyword: 'int'
Memory: 4 bytes, range from -2^31 to 2^31 - 1.
```
- Character 字符类型
```
Keyword: 'char'
Memory: 1 byte, range from -2^7 to 2^7 - 1 or 0 to 2^8 - 1
```
- Boolean 布尔
```
Keyword: 'bool'
A boolean variable can store either true or false.
```
- Floating Point 单精度浮点类型
```
Keyword: 'float'
Memory: 4 byte
```
- Double Floating Point 双精度浮点
```
Keyword: 'double'
Memory: 8 byte
```
- Valueless or Void 无值或空类型
```
Keyword: 'void'
Void data type id used for those function which does not return a value.
```
- Wide Character 宽字符（？）
```
Keyword: 'wchar_t'
Memory: it is generally 2 or 4 bytes long.
```

##### Datatype Modifiers 类型修饰符
- Signed

- Unsigned

- Short

- Long


| DataType               | Size(in bytes) | Range             |
| ---------------------- | -------------- | ----------------- |
| short int              | 2              | -2^15 to 2^15 - 1 |
| unsigned short int     | 2              | 0 to 2^16 - 1     |
| int                    | 4              | -2^31 to 2^31 - 1 |
| unsigned int           | 4              | 0 to 2^32 - 1     |
| long int               | 8              | -2^63 to 2^63 - 1 |
| unsigned long int      | 8              | 0 to 2^64 - 1     |
| long long int          | 8              | -2^63 to 2^63 - 1 |
| unsigned long long int | 8              | 0 to 2^64 - 1     |
| signed char            | 1              | -2^7 to 2^7 - 1   |
| unsigned char          | 1              | 0 to 2^8 -1       |
| float                  | 4              |                   |
| double                 | 8              |                   |
| long double            | 16             |                   |
| wchar_t                | 4              | 1 wide character  |

> Note Above values may very from compiler to compiler. In above example, we
have considered GCC 64 bit and gcc version is 5.4.0 .

> 1 byte == 8 bit (1字节等于8比特)

We can display the size of all the data types by using the sizeof() function
and passing the keyword of the datatype as argument to this function as
showing below:
```
// C++ program to sizes of data types
#include<iostream>
using namespace std;

int main()
{
    cout << "Size of char : " << sizeof(char) << " byte" << endl;
    cout << "Size of int : " << sizeof(int) << " bytes" << endl;
    cout << "Size of short int : " << sizeof(short int) << " bytes" << endl;
    cout << "Size of long int : " << sizeof(long int) << " bytes" << endl;
    cout << "Size of long long int : " << sizeof(long long int) << " bytes" << endl;
    cout << "Size of signed long int : " << sizeof(signed long int) << " bytes" << endl;
    cout << "Size of unsigned long int : " << sizeof(unsigned long int) << " bytes" << endl;
    cout << "Size of float : " << sizeof(float) << " bytes" <<endl;
    cout << "Size of double : " << sizeof(double) << " bytes" << endl;
    cout << "Size of long double : " << sizeof(long double) << " bytes" << endl;
    cout << "Size of wchar_t : " << sizeof(wchar_t) << " bytes" <<endl;

    return 0;
}
```

Output:
```
Size of char : 1 byte
Size of int : 4 bytes
Size of short int : 2 bytes
Size of long int : 8 bytes
Size of long long int : 8 bytes
Size of signed long int : 8 bytes
Size of unsigned long int : 8 bytes
Size of float : 4 bytes
Size of double : 8 bytes
Size of long double : 16 bytes
Size of wchar_t : 4 bytes
```

#### Abstract or user defined data type 抽象或用户自定义数据类型

比如自定义类或结构体
