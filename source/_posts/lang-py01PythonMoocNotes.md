---
title: Python Mooc笔记
date: 2020-01-01 23:00:00
id: py1
categories:
- lang
tags:
- py
---



大一下学期，2020年上半年，疫情在家上网课，当时看的Python所做的笔记。

Python常用的语法，各种库的应用以及主函数的定义。



<!-- more -->



# Python MOOC

### 数据类型

##### 不确定尾数

十进制转化成二进制，产生误差，转化回十进制时，会产生不确定尾速10**-16

0.1 + 0.2 == 0.3     ----> False

round( 0.1 + 0.3 ) == 0.3 ---->True

##### 科学计数法

<a>e<b> == a*(10**b)

##### 复数

a + b j

z.real  ---->获得实部

z.imag  ---->获得虚部

##### 字符串

![](C:\Users\10956\Desktop\微信截图_20200318204634.png)



### 运算

##### 数值运算

abs(value)   绝对值

divmod(x,y)   返回(商,余数)

pow(a,b,z)   a**b%z

round(x,a)    四舍五入几位



### time 库的使用

##### 获取时间

time.time()    浮点数

time.ctime()    人能看

time.gmtime()    计算机可处理

##### 时间格式化

 time.shrftime(tpl , ts)

###### 					time.shrftime("%Y-%m-%d  %H:%M:%S" , time.gmtime )

###### %Y    %m数字    %B%b英文    %d    %A%a星期    %H 24h  %I 12h     %p  pmam    %M    %S

time.strptime(str , tpl)

##### 程序计时

time.perf_counter()

​	start = ...    end = ...   time = end - start

 sleep(s)

##### perf_counter()和process_time()的不同

它们常用于对一段代码计算运行时间

perf_counter()会记录sleep()的时间

而process_time()不会



### timeit模块

timeit . timeit ( function  ,  count )  执行function ,次数为count次 , 返回运行的时间



### tqmd模块:进度条配置模块

tqmd.tqmd( range() )    



### 程序控制结构

##### if ...else   的紧凑模式（三元表达式）

例如：  print( " { } " .format{ "对" if  num > 10 else "错"  }  )

##### 异常处理结构

```python
try:
    < >        
except:
    < >				#如果try语句出现异常，则运行这个内容
else:
    < >				#如果不出现异常，奖励性运行这个内容
finally:
    < >				#最后一定要运行的，无论有没有发生异常
```

##### print 的一个使用

以 某个字符 结尾：print( i , end = "   char  "  )



### Random 库

##### 基本函数

random .seed(  )  如果没有参数，则默认是随系统时间改变，不可复现

​							如果有参数，则是某以固定的随机序列，每次重新调用的时候，都是一样的随机数。

random .random()  是0到1的随机数

##### 扩展随机数函数

```python
random.ranint( a , b )    #产生一个[a,b]之间的整数
random.shuffle( seq ) 	  #对序列seq进行重新排序
random.choice( seq )	  #返回一个seq的元素
random.ranrange(a,b[,c])  #产生一个a到b，步长为c的整数
random.uniform(a , b) 	  #产生一个[a,b]之间的小数
random.getranbits(k)  	  #产生一个k比特长的随机整数
```

### _ _name__  =='_  _ _ main_ _'

如果没有的话,程序就会从第一个函数开始执行

main函数调用这个函数之后,又会执行一遍

如果用了这个的话,程序就会在main函数开始执行







## jieba库的使用

### jieba.lcut(str, cut_all = False)

### jieba.cut_for_search( str )



## wordcloud库

生成一个word cloud对象	w = wordcloud.WordCloud(width=400, height=200, font_size=2, font_path=None, max_font=根据高度自动调节, min_font=4, background_color="black", font_step=2, max_words=200, stop_words={"","} , mask=)

w.generate(str)

w.to_file(filename)