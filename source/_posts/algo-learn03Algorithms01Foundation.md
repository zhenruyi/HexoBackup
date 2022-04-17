---
title: 《算法》笔记：第1章  基础
date: 2022-04-11 15:53:17
id: algorithms1
categories:
- algo
tags:
- learn
---



《算法》第1章：基础。

基础编程模型，数据抽象，背包、队列和栈，算法分析，案例研究。



<!-- more -->



---



算法是适合用计算机实现的解决问题的方法。和算法关系最密切的是数据结构，数据结构是便于算法操作的组织数据的方法。

本章内容：

- 基础编程模型：语法，语言特性，库；
- 数据抽象：抽象数据类型，模块化编程；
- 三种基础的抽象数据类型：背包、队列和栈；
- 算法分析：性能；
- 例子：union-find算法。

---

### 1.1 基础编程模型

使用编程语言实现算法，出于以下原因：

- 程序是对算法精确、优雅和完全的描述；
- 通过运行程序学习算法的各种性质；
- 直接使用这些算法。

这样做的一个缺点是，使用特定语言，使分离算法的思想和实现细节变得困难。

基础编程模型：描述和实现算法所用到的语言特性、软件库和操作系统特性的总称。

#### 1.1.1 程序的基本结构

语法，是大多数现代语言共有的：

- 原始数据类型：精确定义了整数、浮点数和布尔值，定义包括取值范围和操作。
- 语句：六种语句，包括声明、赋值、条件、循环、调用和返回。
- 数组、字符串。
- 函数/方法。
- 标准输入输出。
- 数据抽象：数据抽象封装和重用，定义非原始数据类型，进而支持面向对象编程。

####  1.1.2 原始数据类型与表达式

语言的基础知识：表达式、类型转换、比较和其他原始数据类型。

#### 1.1.3 语句

六种语句。

#### 1.1.4 简便记法

目的：追求清晰、优雅和高效的代码：

- 声明并初始化。在golang中，使用符号:=。
- 隐式赋值：i++，+=。

#### 1.1.5 数组/切片

顺序存储同类型的多个数据。

- 创建并初始化：注意初始值。
- 注意指针和引用。
- 二维数组

#### 1.1.6 方法/函数

外部库使用import导入。

#### 1.1.7 API

模块化编程的一个重要的组成部分就是记录库方法的用法并提供其他人参考的文档。统一使用应用程序编程接口。

#### 1.1.8 字符串

字符串拼接+，类型转换strconv。

自动转换：+的一边是字符串，会自动将其他转换成字符串。

#### 1.1.9 输入输出

标准输入输出：fmt。

#### 1.1.10 二分查找

#### 1.1.11 展望

数据抽象，有时也被称为面向对象编程。使用数据抽象的理由：

- 允许通过模块化编程复用代码。
- 轻易构造更多链式数据结构，它们比数组更灵活，是高效算法的基础。
- 准确定义算法问题。

---



### 1.2 数据抽象

数据类型：一组值和一组对这些值的操作的集合。

数据抽象：定义和使用数据类型的过程。

抽象数据类型：封装后的数据类型。

#### 1.2.1 使用抽象数据类型

要使用一种数据类型并不一定非得知道它是怎么实现的。

#### 1.2.2 抽象数据类型举例

各类库。

#### 1.2.3 抽象数据类型的实现

- 实例变量：类的实例。
- 构造函数：跟类同名的函数。
- 实例方法。
- 作用域：参数变量，局部变量，实例变量。

#### 1.2.4 更多抽象数据类型的实现

第三方库。

#### 1.2.5 数据类型的设计

抽象数据类型是一种向用例隐藏内部表示的数据类型。这种思想强有力地影响了现代编程。

- 封装：并不需要知道怎么实现的。
- 设计API：构建现代软件最重要也是最有挑战的一项任务就是设计API。
- 算法与抽象数据类型。
- 接口继承。
- 实现继承。
- 等价性。
- 内存管理。
- 不可变性。
- 异常处理。
- 断言。



---



### 1.3 背包、队列和栈

许多基础数据类型都和对象的集合有关，所有的操作都是对对象的增删改查。

三种数据类型：背包(Bag)、队列(Queue)、栈(Stack)，它们不同之处就是删除或者访问对象的顺序不同。

本节目标：

- 说明对集合的表示方法，直接影响到各种操作的效率，要设计适用于对象的数据结构并高效地实现所需要的方法。
- 介绍泛型和迭代，Java概念。
- 说明链式数据结构的重要性，特别是经典的链表，有了它才能高效实现上述三种数据结构。

#### 1.3.1 API

| Bag                                                | Queue         | Stack      |
| -------------------------------------------------- | ------------- | ---------- |
| NewBag()<br />go语言没有构造函数，所以使用该方法。 | NewQueue()    | NewStack() |
| add(item)                                          | enQueue(item) | push(item) |
|                                                    | deQueue()     | pop()      |
| isEmpty()                                          | isEmpty()     | isEmpty()  |
| size()                                             | size()        | size()     |

##### 1.3.1.1 泛型

只需要一份API就能处理所有类型的数据。

go1.18开始支持泛型。

##### 1.3.1.2 自动装箱

自动将一个原始数据类型转换为一个封装类型被称为自动装箱。例如，int -> Interger。

自动拆箱。

##### 1.3.1.3 可迭代的集合类型

处理集合中的每一个元素，或者叫做迭代访问集合中的所有元素。

```go
切片：
for index, value := range slice {

}
字典：
for key, value := range map{

}
```

##### 1.3.1.4 背包

- 不支持删除元素的集合数据类型。
- 目的：帮助收集元素并迭代遍历所有元素。迭代的顺序不确定且与用例无关。
- 也可以使用队列和栈，只用背包说明处理顺序不重要。

##### 1.3.1.5 队列

- 先进先出。
- 可以使用数组实现，循环的指针。可以使用链表实现。

##### 1.3.1.6 栈

下压栈，简称栈。

##### 1.3.1.7 算术表达式

如何按照正确的顺序处理算术表达式。20世纪60年代，Dijkstra发明了一个非常简单的算法，使用两个栈，一个保存运算符，一个保存操作数。

- 将操作数压入操作数栈。
- 将运算符压入运算符栈。
- 忽略左括号。
- 遇到右括号，弹出一个运算符，弹出所需数量的操作数，并将运算结果压入操作数栈。

```go
// Dijkstra的双栈算术表达式求值算法
func Evaluate(exp string) float64 {
	// 双栈
	ops := list.New()
	vals := list.New()
	// 处理数字
	val := ""
	for i := 0; i < len(exp); i++ {
		// 不处理空格和(
		if exp[i] == ' ' || exp[i] == '('{
			continue
		}
		// 如果是数字，则拼接
		val += string(exp[i])
		if i+1 < len(exp) && isNum(exp[i]) && isNum(exp[i+1]) {
			continue
		}
		// 算术表达式处理
		switch {
		// 数字的处理
		case len(val) > 1 || (exp[i] >= '0' && exp[i] <= '9'):
			v, _ := strconv.ParseFloat(val, 64)
			vals.PushBack(v)
		// 运算符的处理
		case exp[i] == '+' || exp[i] == '-' || exp[i] == '*' || exp[i] == '/':
			ops.PushBack(exp[i])
		// 遇到反括号，进行一次运算
		case exp[i] == ')':
			// 运算符出栈
			curOp := ops.Remove(ops.Back()).(uint8)
			// 操作数出栈
			curVal2 := vals.Remove(vals.Back()).(float64)
			curVal1 := vals.Remove(vals.Back()).(float64)
			switch curOp {
			case '+': vals.PushBack(curVal1 + curVal2)
			case '-': vals.PushBack(curVal1 - curVal2)
			case '*': vals.PushBack(curVal1 * curVal2)
			case '/': vals.PushBack(curVal1 / curVal2)
			}
		default:
		}
		val = ""
	}
	return vals.Front().Value.(float64)
}
// 判断是不是数字
func isNum(val uint8) bool {
	if val >= '0' && val <= '9' {
		return true
	}
	// 可能是浮点数
	if val == '.' {
		return true
	}
	return false
}
```

#### 1.3.2 集合类数据类型的实现

在讨论Bag、Stack和Queue的实现之前，先给出一个简单而经典的实现，它的改进就得到我们所要的结果。

##### 1.3.2.1 定容栈

表示容量固定的字符串栈，只处理string，需要指定一个容量且不支持迭代。

| FixedCapStackOfStrings             |                         |
| ---------------------------------- | ----------------------- |
| newFixedCapStackOfStrings(cap int) | 创建一个容量为cap的空栈 |
| push(item)                         | 添加一个字符串          |
| pop()                              | 删除最近添加的字符串    |
| isEmpty()                          | 栈是否为空              |
| size()                             | 字符串数量              |

```go
type FixedCapStackOfStrings struct {
	Strs []string
	N int
}

func NewFixedCapStackOfStrings(capacity int) *FixedCapStackOfStrings {
	return &FixedCapStackOfStrings{
		N: capacity,
		Strs: make([]string, 0),
	}
}

func (s *FixedCapStackOfStrings) IsEmpty() bool {
	return len(s.Strs) == 0
}

func (s *FixedCapStackOfStrings) Size() int {
	return len(s.Strs)
}

func (s *FixedCapStackOfStrings) Push(item string) bool {
	if s.Size() >= s.N {
		return false
	}
	s.Strs = append(s.Strs, item)
	return true
}

func (s *FixedCapStackOfStrings) Pop() string {
	if s.Size() == 0 {
		return ""
	}
	res := s.Strs[s.Size()-1]
	s.Strs = s.Strs[:s.Size()-1]
	return res
}
```

##### 1.3.2.2 泛型（这里用interface{}）

```go
type FixedCapStack struct {
	data []interface{}
	capa int
}

func NewFixedCapStack(capacity int) *FixedCapStack {
	return &FixedCapStack{
		capa: capacity,
		data: make([]interface{}, 0),
	}
}

func (s *FixedCapStack) IsEmpty() bool {
	return len(s.data) == 0
}

func (s *FixedCapStack) Size() int {
	return len(s.data)
}

func (s *FixedCapStack) Push(d interface{}) bool {
	if len(s.data) >= s.capa {
		return false
	}
	s.data = append(s.data, d)
	return true
}

func (s *FixedCapStack) Pop() interface{} {
	if s.Size() == 0 {
		return nil
	}
	res := s.data[s.Size()-1]
	s.data = s.data[:s.Size()-1]
	return res
}
```

##### 1.3.2.3 调整数组大小

使用一个resize方法。

```go
func (s *FixedCapStack) Resize(size int) {
	s.capa *= 2
}
```

##### 1.3.2.4 对象游离

在Java中，被弹出的元素的引用还在数组中，这个元素已经不会再被访问，但Java垃圾收集器没办法知道这一点，除非引用被覆盖。

解决办法：弹出时设为null。

#### 1.3.3 链表

链表是一种递归的数据结构，它或者为空，或者指向下一个节点的引用。

##### 1.3.3.1 结点记录

```go
type Node struct {
    Data interface{}
    Next *Node
}
```

##### 1.3.3.2 构造链表

```go
NodeName := new(Node)
NodeName.data = interface{}
NodeName.Next = .......
```

##### 1.3.3.3 表头插入结点

```go
NewNode := new(Node)
NewNode.Next = first
first = NewNode
```

##### 1.3.3.4 从表头删除结点

```go
first = first.Next
```

##### 1.3.3.5 从表尾插入结点

```go
Last := new(Node)
OldLast.Next = Last
```

##### 1.3.3.6 其他位置的插入和删除操作

```
先遍历，找到位置进行插入和删除操作。
```

##### 1.3.3.7 遍历操作

```go
for p := first; p ! = nil; p = p.Next {
    do something
}
```

##### 1.3.3.8 栈的实现

```go
type Node struct {
	data interface{}
	next *Node
}

type ListStack struct {
	first *Node
	length int
}

func (l *ListStack) IsEmpty() bool {
	return l.length == 0
}

func (l *ListStack) Size() int {
	return l.length
}

func (l *ListStack) Push(elem interface{}) {
	node := new(Node)
	node.data = elem
	node.next = l.first
	l.first = node
	l.length++
}

func (l *ListStack) Pop() interface{} {
	ret := l.first
	l.first = l.first.next
	l.length--
	return ret.data
}
```

##### 1.3.3.9 队列的实现

```go
type ListQueue struct {
	first *Node
	last *Node
	length int
}

func (l *ListQueue) IsEmpty() bool {
	return l.length == 0
}

func (l *ListQueue) Size() int {
	return l.length
}

func (l *ListQueue) Enqueue(item interface{}) {
	node := new(Node)
	node.data = item
	node.next = nil
	if l.length == 0 {
		l.first = node
		l.last = node
	} else {
		l.last.next = node
		l.last = node
	}
	l.length++
}

func (l *ListQueue) Dequeue() interface{} {
	if l.IsEmpty() {
		return nil
	}
	ret := l.first.data
	l.first = l.first.next
	l.length--
	if l.IsEmpty() {
		l.last = nil
	}
	return ret
}
```

##### 1.3.3.10 背包的实现

```go
type ListBag struct {
	first *Node
}

func (l *ListBag) Add(item interface{}) {
	node := new(Node)
	node.data = item
	node.next = l.first
	l.first = node
}

// 迭代，返回一个切片
func (l *ListBag) Iterator() []interface{} {
	ret := make([]interface{}, 0)
	for node := l.first; node != nil; node = node.next {
		ret = append(ret, node.data)
	}
	return ret
}
```



#### 1.3.4 综述

- 数组
  - 优点：通过索引直接访问任意元素。
  - 缺点：初始化需要知道元素的数量，但在go可以使用切片。
- 链表
  - 使用空间大小和元素数量成正比。
  - 需要通过遍历访问元素。



---



### 1.4 算法分析

#### 1.4.1 科学方法

爱因斯坦：“再多的实验也不一定能够证明我是对的，但只需要一个实验就能证明我是错的。”

我们永远也没法知道某个假设是否绝对正确，我们只能验证它和我们的观察的一致性。

#### 1.4.2 观察

计算性任务的困难程度可以用问题的规模来衡量。使用不同的规模来观察计算性任务的变化。

#### 1.4.3 数学模型

尽管很多复杂因素影响运行时间，原则上我们仍然可能构造出一个数学模型来描述任意程序的运行时间。Knuth认为，一个程序运行的总时间主要和两点有关：

- 执行每条语句的耗时；
- 执行每条语句的频率。

前者取决于计算机、编译器和操作系统，后者取决于程序本身和输入。

##### 1.4.3.1 近似

首项之后的其他项相对较小，使用约等于号(~)来忽略较小的项。

| 函数                      | 近似     | 增长数量级 |
| ------------------------- | -------- | ---------- |
| N^3 / 6 + N^2 / 2 + N / 3 | ~N^3 / 6 | N^3        |
| lg N + 1                  | ~lg N    | lg N       |
| 3                         | ~3       | 1          |

##### 1.4.3.2 近似运行时间

许多程序的运行时间都只却决于其中的一小部分指令。

##### 1.4.3.3 对增长数量级的猜想

![](https://zhenruyi.github.io/images/algo-learn03Algorithms01Foundation1.png)

#### 1.4.4 增长数量级的分类

![](https://zhenruyi.github.io/images/algo-learn03Algorithms01Foundation2.png)

- 常数级别：不依赖于N。
- 对数级别：比常数时间稍慢，对数的底数和增长的数量级无关。
- 线性级别：单个for循环，增长时线性的，和N成正比。
- 线性对数级别：常见的是归并排序和快排。
- 平方级别：两个嵌套的for循环。
- 立方级别：三个嵌套的for循环。
- 指数界别：不可能用于解决大规模的问题，但某些领域也很重要。

#### 1.4.7 注意事项

- 大常数：公式的系数如果很小就可以忽略，但是很大就不要忽略。
- 非决定性的内循环：有些程序在内循环之外也有大量指令需要考虑。
- 指令时间：每条指令所需的时间不同。
- 系统因素：只是计算机争夺资源的众多应用程序之一。
- 不分伯仲：有些程序员喜欢投入大量精力找出“最佳”实现，这类工作最好还是留给专家。

---



### 1.5 案例研究：union-find算法

合并-查找，应用于连通性问题当中。

#### union-find的实现

```go
type UnionFind struct {
	id []int
	count int
}

func NewUnionFind() *UnionFind {
	return &UnionFind{
		id: nil,
		count: 0,
	}
}

func (uf *UnionFind) Count() int {
	return uf.count
}

func (uf *UnionFind) Connected(p, q int) bool {
	return find(p) == find(q)
}

func (uf *UnionFind) find(p int) int {
}

func (uf *UnionFind) union(p, q int) {
}
```

#### union方法和find方法的实现

##### quick-find算法

```go
func (uf *UnionFind) QuickFindFind(p int) int {
	return uf.id[p]
}

// 将p和q归并到相同的分量中
func (uf *UnionFind) QuickFindUnion(p, q int) {
	// p和q的分量
	pID := uf.find(p)
	qID := uf.find(q)
	// 相同则返回
	if pID == qID {
		return
	}
	// 将和p分量相同的变成q的分量
	for i := 0; i < len(uf.id); i++ {
		if uf.id[i] == pID {
			uf.id[i] = qID
		}
	}
	// 分量减少一个
	uf.count--
}
```

find()的操作很快，但是quick-find算法无法处理大型问题，因为对于每一次union都需要扫描整个id切片。

##### quick-union算法

```go
func (uf *UnionFind) QuickUnionFind(p int) int {
	// 找到根触点
	for p != uf.id[p] {
		p = uf.id[p]
	}
	return p
}

func (uf *UnionFind) QuickUnionUnion(p, q int) {
	pRoot := uf.QuickUnionFind(p)
	qRoot := uf.QuickUnionFind(q)
	if pRoot == qRoot {
		return
	}
    // 只需要修改根触点的指向就行
	uf.id[pRoot] = qRoot
	uf.count--
}
```



##### 加权quick-union算法

```go
type WeightedQuickUnionUF struct {
	id []int
	size []int
	count int
}

func (uf *WeightedQuickUnionUF) Count() int {
	return uf.count
}

func (uf *WeightedQuickUnionUF) connected(p, q int) bool {
	return uf.find(q) == uf.find(q)
}

func (uf *WeightedQuickUnionUF) find(p int) int {
	for p != uf.id[p] {
		p = uf.id[p]
	}
	return p
}

func (uf *WeightedQuickUnionUF) union(p, q int) {
	pRoot := uf.find(p)
	qRoot := uf.find(q)
	if pRoot == qRoot {
		return
	}
	if uf.size[qRoot] < uf.size[pRoot] {
		uf.id[qRoot] = pRoot
		uf.size[pRoot] += uf.size[qRoot]
	} else {
		uf.id[pRoot] = qRoot
		uf.size[qRoot] += uf.size[pRoot]
	}
	uf.count--
}
```

##### 性能特点

| 算法                 | union()  | find()   |
| -------------------- | -------- | -------- |
| quick-find           | N        | 1        |
| quick-union          | 树的高度 | 树的高度 |
| weighted quick-union | log      | log      |







---

