---
title: Bubble List项目备忘
date: 2022-02-02 23:00:00
id: go1
categories:
- lang
tags:
- go
---



Golang语言gin框架项目Bubble List的笔记



<!-- more -->



todo module: struct



var DB *gorm.DB

​	database object



initMySQL

gorm.Open(dialect string, dsn string)

​	dialect: nickname

​	dsn: username:password@tcp(host:port)/dbname?charset=utf8mb4&parTime=True&loc=Local

​		utf8mb4 = utf8 more bytes 4

defer DB.Close()



init gin router engine

​	call Static method

​	Call LoadHTMLFiles method

​	call GET method: pass back a HTML file(index.html)



gin router group: call Group method

​	POST: add

​		new Todo obj

​		bind to handler

​		return context

​	GET: view

​		new Todo slice

​		





engine run