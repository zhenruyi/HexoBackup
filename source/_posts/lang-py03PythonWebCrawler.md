---
title: Python网络爬虫和信息提取
date: 2020-01-01 23:33:00
id: py3
categories:
- lang
tags:
- py
---



Python爬虫和信息提取：[8天搞定Python爬虫开发](https://www.bilibili.com/video/BV1x54y1d7ny)



<!-- more -->

# 网络爬虫和信息提取

1. Requests: 自动爬取网页, 自动提交请求
2. robots.txt: 网络爬虫排除标准
3. BeautifulSoup: 解析HTML页面



## requests库

### requests库入门

the website is the API





####  HTTP协议

HTTP : Hypertext Transform Protocol , 超文本传输协议

HTTP基于"请求与响应"模式的 , 无状态的应用层协议

##### URL（Uniform Resource Locator:统一资源定位符),即是网络地址

http://host [ :port] [ path]

host : 合法的Internet主机域名或IP地址

port : 端口号, 默认80

path : 请求资源的路径



#### HTTP协议对资源的操作

GET	请求获取URL的资源

HEAD	请求获取URL的响应报告, 即获取头部信息

POST	附加新的数据

PUT	请求储存一个资源, 覆盖原来的资源

PATCH	局部更新

DELETE	请求删除



#### requests 的7个方法

##### requests.request(P)	设置一个requests请求,是下面7个的支撑

requests.request( method, url, **kwargs)

method : 请求方式, 对应下面6种, 加上OPTIONS

url     : 对应链接

**kwargs : 控制访问的参数, 共13个

​		params : 字典或字节序列, 作为参数添加到url中

​		data : 字典或字节序列或文件对象, 作为Request的内容

​		json : json格式的数据, 作为Request的内容

​		header : 字典, HTTP定制头. 改变浏览器的类型

​		cookies : 字典或cookieJar, Request中的cookie

​		auth : 元组, 支持HTTP的认证功能

​		files : 字典, 传输文件

​		timeout : 设定超时时间, 单位s

​		proxies : 字典, 设置访问代理服务器, 增加认证

​		allow_redirects : Ture或False, 默认True, 重定向开关

​		stream : T或F, 默认T, 获取内容立即下载开关

​		verify : T或F, 默认T, 认证SSL证书开关

​		cert : 本地SSL证书路径



##### requests.get(P)	获取一个网页的内容

##### requests.post( url, data=None, json=None, **kwargs)	在后面接上内容

##### requests.put( url, data=None, **kwargs)	替换全部内容

##### requests.patch( url, data=None, **kwargs)	修改部分内容

##### requests.head( url, **kwargs)	获取头部信息,当整个数据比较大的时候

##### requests.delete( url, **kwargs)	删除



#### (P) stand for (url, params=None, **kwargs)

url           :  网页的地址

params    : 额外参数,以字典或字节流的格式

**kwrags : 12个控制访问的参数



#### requests库的两个对象

r = requests.get(P)

r : Response 包含爬虫返回的内容, 也包含Request信息

get(P) : Request 



#### Respones对象的属性

r.status_code	返回一个状态值, 200则代表连接成功, 404或其他表示失败

r.content	返回内容的二进制格式

r.encoding	返回编码格式, 从header猜测, 可以改变. 如果hearder不存在charset, 则默认为ISO-8859-1

r.apparent_encoding	如果上一个不正确, 则从内容中猜测编码形式

r.text	根据encoding格式返回内容



#### Requests库的异常

requests.Timeout	请求URL超时

requests.ConnectTimeout	网络连接超时

requests.HTTPError	HTTP错误异常

requests.ConnectionError	网络连接错误异常, 如DNS查询失败, 拒绝连接等

requests.TooManyRedicrets	超过最大重定向次数

requests.URLRequired	URL缺失



#### Resopnse异常

r.raise_for_status()	如果返回状态值不是200, 则产生一个错误信息requests.HTTPError

#### 爬取网页的通用代码 : 注重异常处理

def getHTMLText (url) :

​        try:

​				r = requests.get(P)

​				r.raise_for_status()

​				r.encoding = r.apparent_encoding

​				return r.text

​		except

​				return "产生异常"



### 盗亦有道

#### 网络爬虫的尺寸

小规模(爬取网页\玩转网页): requests库

中规模\对速度敏感: Scrap库

大规模\搜索引擎: 定制开发



#### 网站对爬虫的限制

##### 来源审查: 判断User-Agent进行限制

检查来访的HTTP header头User-Agent域, 只响应浏览器或者友好爬虫的访问

##### 发布公告: Robots协议

告知所有爬虫的爬取策略, 要求爬虫遵守

根目录下的robots.txt文件

​	/代表根目录

​	*代表所有

​	

### Requests库网络爬取实战

##### 京东商品

```python
import requests
url = 
try:
	r = requests.get(url)
	r.raise_for_status()
	r.encoding = r.apparent_encoding
	print(r.text[:1000])
except:
	print("爬取失败")
```

##### 亚马逊商品

```python
import requests
url = 
try:
	kv = {"User-Agent": "Mozilla/5.0"}
	r = requests.get(url, headers = kv)
	r.raise_for_status()
	r.encoding = r.apparent_encoding
	print(r.text[...])
except:
	print("error")
```

##### 百度搜索

```python
import requests
url = "www.baidu.com/s"
try:
	kv = {"wd": Keyword}
	r = requests.get(url, params = kv)
	printr(r.requests.url)
	r.
```

##### 图片爬取

```python
import requests
import os

url = 图片地址
root = "保存图片的文件夹"
path = root + url.split('/')[-1]

try:
	r = requests.get(url)
	r.raise_for_status()
	
	if not os.path.exists(root):
		os.mkdir(root)
	if not os.path.exists(root + path)
		with open(path, "wb") as f:
		f.write(r.content)
		f.close()
		print("sucessfully")
	else:
		print("the file is exist")
except:
	print("error")
```





## BeautifulSoup

这个库是解析, 遍历, 维护"标签树"的功能库

### 标签

```
<p class="title"> ... </>  尖括号里包含的内容就是标签
p 标签的名称Name
class 即是标签的一个属性Atrributes
... 是标签的string
```



### 基本元素

#### BeautifulSoup 类

一颗BS 对应一个 HTML/XML 文档的全部内容

#### BS解析器

-   bs4 的HTML 解析器: BeautifulSoup(mk, 'html.parser')
-   lxml 的HTML 解析器: (mk, 'lxml')
-   lxml 的XML 解析器: 'xml'
-   html5lib 解析器: 'html5lib'

#### 基本元素

```python
import requests
from bs4 import BeautifulSoup

url = 
try:
	...
except:
	...
demo = r.text()
soup = BeautifulSoup(demo, 'html.parser')

```



-   Tag	标签

    ​		soup.title

    ​		soup.p 获取标签<p>, 如果有多个, 返回第一个.

    

-   Name    名字    <tap>.name

    ​		soup.p.name

    

-   Attributes    属性    <tap>.attrs

    ​		soup.p.attrs['one of attributes']

    ​		such as 'class', 'href'

    

-   NavigableString    非属性字符串    <tag>.string

    ​		soup.string or soup.p.string

    

-   Commet    注释   

    ​		一种特殊的string



### 基于bs4库的HTML内容遍历方法

HTML的基本格式: 标签树

#### 遍历方式

-   下行
    -   soup.p.contents    子节点的列表
    -   .chrildren    子节点的迭代类型, 用于循环
    -   descendants    子孙节点的迭代类型
-   上行
    -   .parent    父辈
    -   .parents    先辈
-   平行
    -   next_sibiling    下一个平行节点的标签
    -   previous_sibling    上一个平行节点的标签
    -   next_siblings    迭代类型
    -   previous_siblings    迭代类型

#### prettify()方法

soup.prettify()




### 信息标记的三种形式

#### XML   

HTML 是XML 的一个子类

#### JSON

类似字典, 有类型的键值对

#### YAML

无类型的键值对

### 基于bs4的信息提取

-   find()
-   find_parents()
-   find_parent()
-   find_next_siblings()
-   find_next_sibling()
-   find_previous_siblings()
-   find_previous_sibling()



#### soup.find_all(name, attrs, recursive, string, **kwargs)    返回的是一个列表

##### name

标签的名字, 多个的话[a, b].   name=True, 返回所有标签名字

以b 开头的标签, re.compile("b")



##### attrs

标注类型



##### recursive = True

是否对全部子孙遍历



##### string

对字符串区域检索字符串



##### kwrags