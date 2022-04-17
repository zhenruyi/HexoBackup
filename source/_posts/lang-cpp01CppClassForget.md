---
title: C++容易忘的点
date: 2020-01-01 23:00:00
id: cpp1
categories:
- lang
tags:
- cpp
---

C++面向对象中容易忘记的知识点：变量的作用域，static，const，friend。

<!-- more -->



类

```c++
class A{
    //构造函数
    A:a(ai),b(bi){
    }
    //析构函数
    ~A{
        
    }
}
A::A(ai,bi):a(ai),b(bi)
```

变量的作用域	自动局部 < 静态局部 < 全局变量        先定义的后释放

const数据成员的初始化	在构造函数里定义	定义之后就不能改

const成员函数	在结尾加const

static数据成员	是类共有的

static成员函数	只能修改static数据成员	类共有的	在之前加	在类外面不用加

static const数据成员	定义类时就要赋值

友元friend	友元函数,在类里面声明	友元成员,友元类的其中一个成员能访问自己	友元类,友元的每一个成员函数都可以访问自己所有的成员friend class

类可以先声明	后面再定义

​	