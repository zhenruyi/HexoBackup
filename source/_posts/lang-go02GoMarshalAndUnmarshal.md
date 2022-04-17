---
title: Golang序列化和反序列化
date: 2022-03-30 17:42:34
id: go2
categories:
- lang
tags:
- go
---





Golang序列化就是把结构体对象转变成Json数据，反序列化就是把Json数据转换成结构体对象。

关于JSON数据，结构体与JSON序列化，结构体标签，嵌套结构体和JSON序列化。



<!-- more -->



### 一  关于JSON数据

JSON(JavaScript Object Notation，JS对象标记)，一种轻量级的数据交换格式。RESTful API 接口中返回的数据都是JSON数据。



### 二  结构体与JSON序列化

Golang要给app或者小程序提供api接口数据，就需要涉及结构体和json之间的转换。

```
序列化使用 json.marshal(interface{}) ([]byte, error)
反序列化使用 json.unmarshal([]byte, interface{}) (error)
```

```go
import "encoding/json"

// 结构体
type Student struct {
	Id string
	Age int
	Name string
    sex string   // 私有对象不能序列化
}

func main() {
    // 结构体对象
	stu := Student{
		Id: "123",
		Age: 12,
		Name: "luyiz",
        sex: "女",
	}
    // 序列化
	bytes, _ := json.Marshal(stu)
    // 强制转换
	str := string(bytes)
    // 输出结果，没有私有对象，key的首字母大写
    // {"Id":"123","Age":12,"Name":"luyiz"}
	fmt.Println(str)
}
```

```go
type Student struct {
	Id string
	Age int
	Name string
	sex string
}

func main() {
    // 将json数据反序列化，得到一个结构体对象
	str := `{"Id":"123","Age":12,"Name":"luyiz"}`
	bytes := []byte(str)
	stu := Student{}
	_ = json.Unmarshal(bytes, &stu)
    // 类型是一个结构体
    // type: main.Student, data: {123 12 luyiz }
	fmt.Printf("type: %T, data: %v", stu, stu)
}
```



### 三  结构体标签Tag

Tag是结构体的元信息，可以在运行的时候通过反射的机制读取出来。

为结构体编写Tag时，严格遵守键值对的队则。结构体标签的解析容错能力很差，一旦格式错了，编译和运行都不会报错。

不要再key和value之间添加空格。

```go
type Student struct {
	Id string `json:"id"`
	Age int `json:"age"`
	Name string `json:"name"`
	// Struct field 'sex' has 'json' tag but is not exported
	sex string `json:"sex"`
}

func main() {
	stu := Student{
		Id: "123",
		Age: 12,
		Name: "luyiz",
		sex: "女",
	}
	bytes, _ := json.Marshal(stu)
	str := string(bytes)
	// key变成标签的形式
	// {"id":"123","age":12,"name":"luyiz"}
	fmt.Println(str)
}
```



### 四  嵌套结构体和JSON序列化

```go
type Student struct {
	Id string `json:"id"`
	Age int `json:"age"`
	Name string `json:"name"`
}

type Class struct {
	Title string
	Member []Student `json:"member"`
}

func main() {
	stu1 := Student{
		Id: "123",
		Age: 12,
		Name: "luyiz",
	}
	stu2 := Student{
		Id: "122",
		Age: 13,
		Name: "a123",
	}
	member := make([]Student, 0)
	member = append(member, stu1)
	member = append(member, stu2)
	class := Class{
		Title: "1班",
		Member: member,
	}
	bytes, _ := json.Marshal(class)
	str := string(bytes)
	// {"Title":"1班","member":[{"id":"123","age":12,"name":"luyiz"},{"id":"122","age":13,"name":"a123"}]}
	fmt.Println(str)
}
```







