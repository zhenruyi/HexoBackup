---
title: Golang中的Package和go mod
date: 2022-03-30 18:41:16
id: go3
categories:
- lang
tags:
- go
---





go语言中的包管理和go.mod文件。

包的介绍和定义，包管理工具go mod，自定义包，init()初始化函数，第三方包。



<!-- more -->



#### 1 包的介绍和定义

包是源码的集合，是一种代码复用方案。

包分为三种：

- 系统内置：引入后可以直接使用，如fmt，strconv，strings。
- 自定义：自己写的包。
- 第三方：下载到本地才可以使用。如"github.com/shopspring/decimal"。



#### 2 包管理工具go mod

1.11版本之前，需要使用自定义的包时，需要把项目放到GOPATH目录，但是1.11版本之后无需手动配置环境变量，使用go mod管理项目，可以在任何位置新建项目。1.13版本之后可以彻底不要GOPATH了。

```
在任意位置新建一个项目，在此目录下使用
go mod init ProjName
初始化一个go mod文件go.mod
```



#### 3 自定义包：定义，导入

```
定义：新建一个文件夹PackName，然后在该文件夹下的文件中，声明这个文件属于的包：
package PackName
- 建议包名和文件夹名字一样。
- 包的声明一定要在第一行。
- 包内的结构体、函数不能重复定义。
- 包内名称，首字母大写说明是共有的，首字母小写说明是私有的。
- 包名为main的为程序的入口包，编译后会得到一个可执行文件。
- 没有main的包的源代码不会生成一个可执行文件。

导入：import "ProjName/PackName"
使用方法或者变量：PackName.Var，PackName.Func。

引入别名：import NickName "ProjName/PackName"
引入匿名(编译时会嵌入源代码)：import _ "ProjName/PackName"
```



#### 4 init()初始化函数

递归执行init()函数。

```
main:  import packA
packA: import packB
PackB: import packC
PAckC

init()函数的执行顺序
PackC.init() -> packB.init() -> packA.init() -> main.init() -> main()
```



#### 5 第三方包

##### 5.1 找到第三方包

在https://pkg.go.dev找到常用的包。一般是一个GitHub地址。



##### 5.2 安装这个包

第一种方法：go get github.com/....

第二种方法：go mod download

会下载到$GOPATH$/pkg/mod，多个项目会共享缓存的mod。

第三种方法：go mod vendor 将依赖复制到当前项目的vendor下。
