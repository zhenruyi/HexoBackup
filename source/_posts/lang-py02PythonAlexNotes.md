---
title: Python学习日记(Alex老师)
date: 2020-01-01 23:11:00
id: py2
categories:
- lang
tags:
- py
---





跟着Alex老师学的Python，视频链接：[96天从小白炼成PYTHON开发](https://www.bilibili.com/video/BV1j7411e7MD)



<!-- more -->



# Python学习日记

## 第一天

### 字符串

拼接：a+b

次数：a*3

赋值：单引号、双引号、多引号（多行）

### 列表（数组）

添加：插入name.insert(3,'alex')、追加name.append（“tony”）

修改：name[2]=" "

删除：del name[2],name.remove("   ")

查找：in     

查找下标：name.index()返回坐标

### 字符串格式化输出

占位符：%s，%d，%f

![image-20200315220331079](C:\Users\10956\AppData\Roaming\Typora\typora-user-images\image-20200315220331079.png)

### 深圳小事

不要烂在泥土里

贪欲吞噬人性

### 运算符

算数运算：幂**   取整除//

比较运算：

赋值运算：**=、//=

逻辑运算：and、or、not

### while..else循环

如果while没有给break终止的话，执行else后的语句



## 第二天

### 课前鸡汤

复合型人才

### 变量的创建过程

​	a=“alex”

​	b=a

a、b都指向alex而不是b指向a

​	a='alex'

​	a='boy'

此时上下a指向的地址不一样

### 身份运算

is /is not

​	a=‘alex'

​	type(a)   is   string     (true)

None 空值

​	a = None 

​	if a is None :

### 三元运算

变量  =  值A   if   条件A   else   条件B

### 寻找帮助

help()

​	help(names.remove)

获取能进行的操作

​	names.

### 数据类型

列表

https://book.apeland.cn/details/30/

元组：只读列表

​	长度：len()	

字符串：

​	不转义r(原生字符raw)		a = r ' alex\n '     print(a)   得到alex\n

字典：

## 第三天

### bytes类型

​		f = open ( " python learning . txt " , "w" , encoding = "utf - 8" )     用utff-8的格式编码

​		f = open ("    "   ,    "wb"     )      不要加encoding   因为是用二进制的格式打开        	

python 和 pycharm 加载和编码都是默认utf8 

​		str.encode()        ---->得到的是对应的bytes类型， 以   b ’ ‘ 标识

要转成二进制的情况 : 网络传输、写入硬盘

### copy

在字符串、列表和集合中，修改一个字符串会创建一个新的地址，然后把原来的那个删除。

但是在字典中，s = s1   ，s和s1都指向同样的地址（容器）。

​		字典中每一个数据都有一个地址（容器里的物体）。



copy   

​		浅copy     		s1 = s.copy()   只复制第一层，  		当字典里面还有字典的话，改小字典的数据之后，两份都会影响。

​		深copy 			import  copy             s1 = s.deepcopy()    完全复制一份新的

### 编码和解码

编码 ：str , encode("utf-8")   用utf-8编码

解码： str. decode("utf-8")	之前是用utf-8编码的，现在要把utf-8解码出来，解码后是unicode的格式

### 编码转换

在windows系统上，是gbk的方式编码

在mac/linux上，是以utf-8的方式编码

所以传输文件之后，要改变编码格式，不然会出现乱码。

gbk	--->	unicode	--->	utf-8

​		代码实现 utf-8	--->	gbk

```python
#用utf-8格式 写入文件
f = open ( "data.txt" , "w" )
s_uft8 = "你好未来"
f.write ( s_utf8 . encode ("utf-8") )
f.close

#转换
s_unicode = s_utf8 .decode ("utf-8")
s_gbk = s_unicode .encode ("gbk")

#写入文件
f = open ("data.txt" , "wb" )
f.write(s_gbk)
f.close
```

### 函数的定义

默认返回值是None

返回多个，则会返回元组		return 1,2,3,4,5    --->   	 (1,2,3,4,5)

### 函数的参数

参数的定义从右到左，参数的赋值从左到右

形参：相当于临时变量

实参

默认参数：靠右定义



位置参数	

关键参数

​		def  func( age , name , school )

​		func( 22  ,   name="alex" ,  school = "scnu" )   前一个是位置参数，后两个是关键参数

​	优先级：位置参数 > 默认参数/关键参数



非固定参数

​		def  func( name , *args , **kwargs )     args会返回元组，kwargs会返回字典

​		func ( "alex" , 21 , 22 , age = 33 , sex = "female" )     第一个是位置参数，后四个是非固定参数

​											第二三个会存到元组里，最后两个会存到字典里

### 局部变量和全局变量

局部变量和全局变量，即使名字一样，但是地址不一样。

使用时，查找顺序：局部变量>全局变量

​	locals()		返回全部局部变量，以字典的形式。

​	globals()		返会全部变量

在局部引用一个全局变量    声明（如果没有则创建）：global  name  然后再使用    //不建议这么使用

### 局部引用字典、列表

局部的函数里可以修改字典、列表里的数据，但是字典和列表本身时不可以修改的。

### 嵌套函数

函数里面再定义一个函数，这个小函数的作用域只在这个函数里面。临时函数。

### 匿名函数(lambda)

```python
def func(x):
	return x**2

#lambda表达式
ex = lambda x : x**2
```

最复杂是一个三元表达式    

```python
ex = lambda x : x**2 if x>10 else x**3
```

map( func , [   ] )		把列表里的数据依次作为第一个函数的参数执行

```python
put = map ( lambda x:x**2 , [1,2,3,4,5] )
for i in map :
	print(i)
    
输出的是: 1
	     4
    	 9.....
```

### 高阶函数

满足其一则为高阶函数：接受一个函数输入、返回一个函数

​		def  func1 ( .... ) : .....

​		def  func2 ( x , y , f ) :   f (x)+ f(y) .....

​		func2 ( x , y , func2 )

### 函数递归

效率不高，会导致栈溢出

栈类似于队列

### 内置函数

abs	求绝对值

all 	判断列表、字典、集合里面是否有 None 或者 0 。即如果每一个元素都   在 bool() 返回true，则为True。

any 	判断是否有一个满足  bool(x) = True。

ascii 	如果是在ascii表里的，返回原来的字符。如果不在，则返回unicode编码。" \ \ u "开头

bin 		返回这个十进制数字的二进制形式

bool 		判断是否为0和None，如果是，则返回False

bytearray	将bytes类型变成一个可以修改的bytes数组。例如 b [1] = ...是不可以的，转成数组之后可以。

bytes		转化成bytes类型，以b 开头 。  a = bytes ( "中国 " , "utf-8" )   --->a为    b'\xd6\xd0\xb9\xfa'

chr 	返回数字对应的字符	

complex 	返回复数    complex ( 1,2 )    --->  1+2 j

dict	返回一个空字典

dir 	返回能进行的操作（类似帮助）

divmod	除然后取模  --->  divmod( 8,3 )    =    ( 2, 2 )

enumerate 	返回列表的索引和元素。  a = ["alex","kiki"]    enumerate后得到 (0,"alex") (1,"kiki")

eval 	把字符串变成对应的数据类型

exec	把字符串变成可以执行的语句   exec("print ("12345) ")  会打印12345

exit 	退出程序

filter	过滤不满足条件的数据     。    list(filter ( lambda x: x<10 , [1,2,3,4,5,11,22,33] ))
   --->   [1, 2, 3, 4, 5]

float  	强制转换浮点数类型

frozenset	把集合变成不能改的

globals	返回所有变量、函数

hash 	返回一串以hash编码的到的数据

help	帮助。help(hash) 返回关于hash的定义和使用方法。

hex 	16进制

id 	返回数据的地址

input	输入

int	转换整型

isinstance 	判断是否是某个数据类型    isinstance( a , string )

len 	长度

list	返回空列表

locals	返回局部变量

map	map(function , list)  把列表中的数据一个一个带入到函数中

max	最大值

min 	最小值

oct 	返回10进制数的8进制表示

open	打开

ord 	返回字符的ASCII码

print	输出

quit	离开程序

range	一个列表

round	四舍五入

set	返回空集合

sorted	排序

str	转化成字符串

sum 	加法

tuple	返回空元组

type	返回数据类型

zip	可以合并两个列表  a = [1,2,3]   b = ["alex" , "kiki" ]  

​							zip(a,b)   --->   [   (1,"alex") ,  ( 2,"kiki" )    ]   取小的那个

### 名称空间

LEGB

​	locals：局部的，函数内部的

​	enclosing function：嵌套函数最近的父函数

​	globals：全局变量

​	builtins：所有函数，包括内置函数

### 闭包

外层函数返回内层函数

函数运行完，函数的作用域不会消失

调用外层函数的时候，先不执行内部的函数，直接return  内部函数的地址

### 装饰器

问题产生：“开放-封闭”原则

​		封闭：已经实现的函数不能修改

​		开放：对现有函数进行扩展

​	不能改函数名

​	不能改调用方式

语法：

```python
def func1:.....
def func2:.....
    
func1 = func2(func1)
#等于
@func2
def func1:...
```

可以加参数，非固定参数：*args   **kwargs

##### 列表生成式

给一个列表元素都加1的办法

```python
a = [1,3,4,5,6,7]

#for循环
b = []
for i in a:
    b = append(i+1)
    
#第二种循环
for index,i in enumerate(a):
    a[index] = i+1
    
#lambda表达式、map函数
a = list(map(lambda x:x+1,a))

#列表生成式
a = [i+1 for i in a]
```

##### 生成器：惰性算法

用循环，range会首先生成一个列表，占空间

生成器优点：边执行边计算

语法：把列表生成式的[]改成()就好了    p = ( i for i in range(10) )

​		执行：next( p )

循环调用

```
for i in p :
	print( i )
```

##### 函数生成器

把函数里面的return 改成yield

yield  b ： 程序或者循环  暂停，并且返回   b

一个有yield 的函数，可以在中间去执行别的代码，然后再返回来执行

执行方式

```python
next (func)
或者
func. __next__()

可以中途去干别的事情
next(func)
......do something else
next(func)
```

但是此时函数会暂停，并且永不结束。

一般用for来调用，就不会这样了。



发送值给函数生成器

```python
def func(value):
	for i < value:
        a = yield
        
f = func(100)
f.__next__()   #发送一个None给yield
f.send( a )    #发送一个值，并且执行
```

##### 单线程下的多并发

线程：cpu执行任务的单元

多核：多个线程，并行运算

```python
import time

def consumer(name):
    print("%s 准备吃包子啦!" %name)
    while True:
       baozi = yield  # yield可以接收到外部send传过来的数据并赋值给baozi
       print("包子[%s]来了,被[%s]吃了!" %(baozi,name))
        
c = consumer('A')
c2 = consumer('B')
c.__next__() # 执行一下next可以使上面的函数走到yield那句。 这样后面的send语法才能生效
c2.__next__()

print("----老子开始准备做包子啦!----")

for i in range(10):
    time.sleep(1)
    print("做了2个包子!")
    c.send(i)  # send的作用=next, 同时还把数据传给了上面函数里的yield
    c2.send(i)
```

### 迭代器iterator

迭代对象：	1.可以用于for循环的数据类型：set、tuple、list、dic、str

​					  2.迭代器和迭代器函数

可迭代：Interable   可遍历、可循环			用isinstance()判断是不是可迭代对象



迭代器：可以用next()执行下一次的    例如generator

可以用iter()强制转换成迭代器



## 第四天

### OS库：跟系统调用相关

os 模块提供了很多允许你的程序与操作系统直接交互的功能

```c
得到当前工作目录，即当前Python脚本工作的目录路径: os.getcwd()
返回指定目录下的所有文件和目录名:os.listdir()
函数用来删除一个文件:os.remove()
删除多个目录：os.removedirs（r“c：\python”）
检验给出的路径是否是一个文件：os.path.isfile()
检验给出的路径是否是一个目录：os.path.isdir()
判断是否是绝对路径：os.path.isabs()
检验给出的路径是否真地存:os.path.exists()
返回一个路径的目录名和文件名:os.path.split()     e.g os.path.split('/home/swaroop/byte/code/poem.txt') 结果：('/home/swaroop/byte/code', 'poem.txt') 
分离扩展名：os.path.splitext()       e.g  os.path.splitext('/usr/local/test.py')    结果：('/usr/local/test', '.py')
获取路径名：os.path.dirname()
获得绝对路径: os.path.abspath()  
获取文件名：os.path.basename()
运行shell命令: os.system()
读取操作系统环境变量HOME的值:os.getenv("HOME") 
返回操作系统所有的环境变量： os.environ 
设置系统环境变量，仅程序运行时有效：os.environ.setdefault('HOME','/home/alex')
给出当前平台使用的行终止符:os.linesep    Windows使用'\r\n'，Linux and MAC使用'\n'
指示你正在使用的平台：os.name       对于Windows，它是'nt'，而对于Linux/Unix用户，它是'posix'
重命名：os.rename（old， new）
创建多级目录：os.makedirs（r“c：\python\test”）
创建单个目录：os.mkdir（“test”）
获取文件属性：os.stat（file）
修改文件权限与时间戳：os.chmod（file）
获取文件大小：os.path.getsize（filename）
结合目录名与文件名：os.path.join(dir,filename)
改变工作目录到dirname: os.chdir(dirname)
获取当前终端的大小: os.get_terminal_size()
杀死进程: os.kill(10884,signal.SIGKILL)
```

### sys库

```python
sys.argv           命令行参数List，第一个元素是程序本身路径
sys.exit(n)        退出程序，正常退出时exit(0)
sys.version        获取Python解释程序的版本信息
sys.maxint         最大的Int值
sys.path           返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值
sys.platform       返回操作系统平台名称
sys.stdout.write('please:')  #标准输出 , 引出进度条的例子， 注，在py3上不行，可以用print代替
val = sys.stdin.readline()[:-1] #标准输入
sys.getrecursionlimit() #获取最大递归层数
sys.setrecursionlimit(1200) #设置最大递归层数
sys.getdefaultencoding()  #获取解释器默认编码
sys.getfilesystemencoding  #获取内存数据存到文件里的默认编码
```

### time模块

时间戳timestamp：从1970年1月1日到现在过去了多少秒

元组struct_time：年月日时分秒周  一年中第几天  是否是夏令时

UTC (Coordinated Universal Time ,世界协调时)：中国时UTC+8

DST (Daylight Saving Time)：夏令时

```python
time.localtime( [ timestamp ] )：将一个时间戳转换为当前时区的struct_time。若secs参数未提供，则以当前时间为准。
time.gmtime( [ secs ] )：和localtime()方法类似，gmtime()方法是将一个时间戳转换为UTC时区（0时区）的struct_time。
time.time()：返回当前时间的时间戳。
time.asctime([t])：把一个表示时间的元组或者struct_time表示为这种形式：’Sun Oct 1 12:04:38 2019’。如果没有参数，将会将time.localtime()作为参数传入。
time.ctime([secs])：把一个时间戳转化为time.asctime()的形式。如果参数未给或者为None的时候，将会默认time.time()为参数。它的作用相当于time.asctime(time.localtime(secs))。

time.mktime(t)：将一个struct_time转化为时间戳。
time.strftime(format[, t])：把一个代表时间的元组或者struct_time（如由time.localtime()和time.gmtime()返回）转化为格式化的时间字符串。如果t未指定，将传入time.localtime()。举例：time.strftime(“%Y-%m-%d %X”, time.localtime()) #输出’2017-10-01 12:14:23’
time.strptime(string[, format])：把一个格式化时间字符串转化为struct_time。实际上它和strftime()是逆操作。
举例：time.strptime(‘2017-10-3 17:54’,”%Y-%m-%d %H:%M”) #输出 time.struct_time(tm_year=2017, tm_mon=10, tm_mday=3, tm_hour=17, tm_min=54, tm_sec=0, tm_wday=1, tm_yday=276, tm_isdst=-1)

time.sleep(secs)：线程推迟指定的时间运行,单位为秒。
```

### datatime模块

相比于time模块，datetime模块的接口则更直观、更容易调用

```
datetime.date：表示日期的类。常用的属性有year, month, day；

datetime.time：表示时间的类。常用的属性有hour, minute, second, microsecond；

datetime.datetime：表示日期时间。

datetime.timedelta：表示时间间隔，即两个时间点之间的长度。

datetime.tzinfo：与时区有关的相关信息。（这里不详细充分讨论该类，感兴趣的童鞋可以参考python手册）
```

```python
1. d=datetime.datetime.now() 返回当前的datetime日期类型
d.timestamp(),d.today(), d.year,d.timetuple()等方法可以调用

2. datetime.date.fromtimestamp(322222) 把一个时间戳转为datetime日期类型

3. 时间运算
>>> datetime.datetime.now()
datetime.datetime(2017, 10, 1, 12, 53, 11, 821218)
>>> datetime.datetime.now() + datetime.timedelta(4) #当前时间 +4天
datetime.datetime(2017, 10, 5, 12, 53, 35, 276589)
>>> datetime.datetime.now() + datetime.timedelta(hours=4) #当前时间+4小时
datetime.datetime(2017, 10, 1, 16, 53, 42, 876275)

4.时间替换
>>> d.replace(year=2999,month=11,day=30)
datetime.date(2999, 11, 30)
```

### pickle  &&  json

序列化：数据的 网络传输和储存在硬盘 的形式是 bytes类型。把各种数据类型转化成可以网络传输和储存的类型称为序列化。

反向过程叫做 反序列化

```python
#pickle

str = pickle.dumps( data )   #把data转化成python可识别的字符串

pickle.dump(data,file)		#把data以字符串写入file种

#file = open("  " , rb)
#json时，open(" " , r )     		
pickle.loads( str )			#把str反序列化

pickle.load( file )			#从文件加载

#遵循先进先出的原则
```

```
Json模块也提供了四个功能：dumps、dump、loads、load，用法跟pickle一致
```

pickle 和 json的区别

- JSON:

  优点：跨语言(不同语言间的数据传递可用json交接)、体积小

  缺点：只能支持int\str\list\tuple\dict

  

  Pickle:

  优点：专为python设计，支持python所有的数据类型

  缺点：只能在python中使用，存储数据占空间大

### hashlib

#### HASH加密

一般译作散列或者哈希。是把任意输入（预映射）转化成固定长度（128位）的输出，这个输出称之为散列值。这是一种压缩算法。

#### 密码学相关

碰撞：不同字符串通过hash算法得到相同的散列。

撞库：用穷举法反解散列值，以获得原来的明文密码。

加盐：通过给hash得到的散列通过加盐算法增加字符然后再次hash。

拖库：黑客获取了密码库。

#### MD5(Message-Digest Algorithm)

讯息摘要演算法。一种加密算法。

##### MD5的特点

- 压缩性：得到的散列一般比原数据 占内存小
- 易计算：通过MD5的算法，计算时间短
- 抗修改：修改原数据，将得到不同的HASH值
- 抗碰撞：一般不会有相同的HASH值
- 不可逆

##### MD5的效果

1. 防篡改：发送和接受时的HASH值一样，则没有被篡改
2. 防抵赖：申请数字签名
3. 防看到明文：看不到密码

##### MD5的操作

```python
import hashlib
#获取一个md5对象
m = hashlib.md5()
#给md5对象一个值，要bytes类型。多次update是将字符串拼接
m .update("str".encode("type"))
#默认得到是二进制，也可以转化成十六进制
m .hexdigest()
```

#### SHA(Secure hash Algorithnm)

sha - 1 :得到160位的散列值。

sha - 256：得到256位。

一般用在密码学上，操作和MD5一样。

### shutil模块

```python
#shutil.copyfileobj ( open(fsrc, "rb"), open(fdes, "wb") )
shutil.copyfileobj(open("d:\\my1.txt", "rb"), open("d:\\my2.txt", "wb"))

#shutil.copyfile("file1" , "file2") ，f2非必须存在

#copy权限
shutil.copymode( fsrc , fdes )

#拷贝状态信息，time、bits...
shutil.copystat( fsrc , fdes )

#拷贝文件和权限
shutil.copy( fsrc , fdes )

#拷贝文件和状态
shutil.copy2(  ,  )

#忽略某种格式
shutil.ignore_patterns(*patterns)
#example: *.txt、filename* ....

#拷贝文件夹
shutil.copytree(src,des,symlinks="False",ignore="False")

#创建压缩包并返回路径
shuil.makearchive( base_name , format , root , )
#base_name：压缩包的路径和名字，若只有名字，则保存到当前目录
#format：压缩包的格式'zip''rar''tar'
#root：要压缩的文件夹的路径

#删除文件夹
shutil.rmtree(  )

#重命名
shutil.move("f1","f2")

```

#### zipfile压缩&解压缩

```python
import zipfile
# 压缩
z = zipfile.ZipFile('laxi.zip', 'w')
z.write('a.log')
z.write('data.data')
z.close()

# 解压
z = zipfile.ZipFile('laxi.zip', 'r')
z.extractall(path='.')
z.close()
```

#### tarfile压缩&解压缩

```python
import tarfile
# 压缩
>>> t=tarfile.open('/tmp/egon.tar','w')
>>> t.add('/test1/a.py',arcname='a.bak')
>>> t.add('/test1/b.py',arcname='b.bak')
>>> t.close()

# 解压
>>> t=tarfile.open('/tmp/egon.tar','r')
>>> t.extractall('/egon')
>>> t.close()
```

### re正则匹配

#### 匹配规则

- re.match()	从第一个字符开始匹配，如果不符合则返回None
- re.search()    匹配全局，返回第一个
- re.findall()      把所有匹配到的字符，放到一个列表返回
- re.split()      以匹配到的字符当做列表分隔符，与findall相反
- re.sub 匹配字符并替换    re.sub( 要替换，替换成，字符串，count=替换次数)
- re.fullmatch    精确匹配，这个字符串必须完全符合规则

#### 表达式规则

```python
'.'     默认匹配除\n之外的任意一个字符，若指定flag DOTALL,则匹配任意字符，包括换行
'^'     匹配字符开头，若指定flags MULTILINE,这种也可以匹配上(r"^a","\nabc\neee",flags=re.MULTILINE)
'$'     匹配字符结尾， 若指定flags MULTILINE ,re.search('foo.$','foo1\nfoo2\n',re.MULTILINE).group() 会匹配到foo1
'*'     匹配*号前的字符0次或多次， re.search('a*','aaaabac')  结果'aaaa'
'+'     匹配前一个字符1次或多次，re.findall("ab+","ab+cd+abb+bba") 结果['ab', 'abb']
'?'     匹配前一个字符1次或0次 ,re.search('b?','alex').group() 匹配b 0次
'{m}'   匹配前一个字符m次 ,re.search('b{3}','alexbbbs').group()  匹配到'bbb'
'{n,m}' 匹配前一个字符n到m次，re.findall("ab{1,3}","abb abc abbcbbb") 结果'abb', 'ab', 'abb']
'|'     匹配|左或|右的字符，re.search("abc|ABC","ABCBabcCD").group() 结果'ABC'
'(...)' 分组匹配， re.search("(abc){2}a(123|45)", "abcabca456c").group() 结果为'abcabca45'
'[...]' 匹配[]范围里面的字符。[0-9]、[a-z]、[0-9a-zA-Z]

'\A'    只从字符开头匹配，re.search("\Aabc","alexabc") 是匹配不到的，相当于re.match('abc',"alexabc") 或^
'\Z'    匹配字符结尾，同$ 
'\d'    匹配数字0-9
'\D'    匹配非数字
'\w'    匹配[A-Za-z0-9]
'\W'    匹配非[A-Za-z0-9]
's'     匹配空白字符、\t、\n、\r , re.search("\s+","ab\tc1\n3").group() 结果 '\t'
'(?P...)' 分组匹配 re.search("(?P<name>[0-9]{4}) (?P<name>[0-9]{2}) (?P<name>[0-9]{4})" , str)  a.groups()  -->返回元组,     a.groupdict() -->返回字典，key是name
```

#### re.compile(pattern, flags=0)

把这个规则先编译，这样就不用每次调用都重新编译

```python
prog = re.compile(pattern)
result = prog.match(string)
```

#### Flags标志符

- re.I (re.IGNORECASE): 忽略大小写（括号内是完整写法，下同）
- re.M (MULTILINE): 多行模式，不会忽略 \n，改变’^’和’$’的行为
- re.S (DOTALL): 改变 ’ . ’ 的行为，能匹配特殊符号
- re.X (re.VERBOSE) 可以给你的表达式写注释，使其更可读，下面这2个意思一样

```
a = re.compile ( r"""\d + # the integral part                
				\. # the decimal point                
				\d * # some fractional digits""",                 
				re.X)
b = re.compile(r"\d+\.\d*")
```

