---
title: 坦黎科技面试
date: 2022-03-10 17:16:09
id: job1
categories:
- other
tags:
- job
---



2022年3月5日早上面试。

2022年3月10日入职。



<!-- more -->





## Golang

### main函数

#### 1. void main(void)能通过编译吗，有什么潜在问题？

```
大多数的编译器都是可以通过的，但是会发出警告。main函数的返回值是int而不是void。int返回类型会让程序返回状态值，这点非常重要，特别是当程序作为依赖于程序成功运行的脚本的一部分运行时。
```

#### 2. 

[main函数_百度百科 (baidu.com)](https://baike.baidu.com/item/main函数/6887703)



### Init函数：外？本包？

[(12条消息) init函数的介绍](https://blog.csdn.net/qq_42303254/article/details/107647925)

[Go语言之init函数 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1608937#:~:text=Go语言有一个特殊的函数init，先于main函数执行，实现包级别的一些初始化操作。 对于init 函数来说：每个包可以包含任意多个 init 函数，这些函数都会在程序执行开始的时候被调用。 所有被编译器发现的,init 函数都会安排在 main 函数之前执行。 init 函数用在设置包、初始化变量或其他要在程序运行前优先完成的引导工作。)



### 引用类型

[Golang 的引用类型底层实现 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/111796041)



### 同步锁

[Go语言 | 并发设计中的同步锁与waitgroup用法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/242105419#)

[(12条消息) Golang同步锁的两种方式_cheene的博客-CSDN博客_go 同步锁](https://blog.csdn.net/weixin_38089997/article/details/108793195)



### channel特性

[Golang教程之管道篇（六） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/85632976)



### 线程和协程

[进程、线程与协程 - FilletNotFish - 博客园 (cnblogs.com)](https://www.cnblogs.com/filletnotfish/p/15057349.html)

[进程和线程、协程的区别 - RunningPower - 博客园 (cnblogs.com)](https://www.cnblogs.com/lxmhhy/p/6041001.html#:~:text=1) 



### 异常 

[go语言之抛出异常 - 传盛 - 博客园 (cnblogs.com)](https://www.cnblogs.com/liucsxiaoxiaobai/p/10805788.html)

除数 panic 空指针

### 选择排序



## Linux

### su和sudo的区别

[(13条消息) sudo与su的区别_风尘仆的博客-CSDN博客_sudo和su的区别](https://blog.csdn.net/frankcreen/article/details/105048051)

[(13条消息) su 命令和sudo命令的区别_-公子世无双~的博客-CSDN博客_su和sudo命令的区别](https://blog.csdn.net/qq_57422382/article/details/120513820)

### 显示当前路径pwd

### 结束进程的命令：kill

[Linux kill命令详解：终止进程 (biancheng.net)](http://c.biancheng.net/view/1068.html)

### 查询后缀名相同的所有文件，然后删除

[(13条消息) linux shell 批量处理相同后缀文件-服务器-CSDN问答](https://ask.csdn.net/questions/324058)



## Mysql

### 索引

[(13条消息) 一文搞懂MySQL索引（清晰明了）_Free Joe的博客-CSDN博客_mysql索引](https://blog.csdn.net/wangfeijiu/article/details/113409719?utm_source=app&app_version=5.2.0)

### 多表查询的方式

[SQL：多表查询 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/91973413)



## Redis



## 工作内容

1. 推荐系统，开源
2. 丰富内容，爬虫
3. IM服务
