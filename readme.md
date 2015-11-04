# Readme

## 概述

codeg是一个轻量级的代码生成器内核（代码仅300行左右），基于Python和jinja2开发，你可以定制自己的项目模板，快速生成可以直接运行的工程项目。

## 快速上手

下载源码
```
https://github.com/lepfinder/codeg
```
执行根目录的codeg.py可以生成demo工程，在target目录中可以查看生成好的代码。
```
#! /usr/bin/env python
# -*- coding: UTF-8 -*-
from core import Manager

manager = Manager("jfinalweb-demo.json")

manager.create()
```
生成器会生成项目的sql文件，手工执行可以完成数据库的创建。


## 创建项目
codeg所有的配置都是json格式。

每一个项目都是一个单独的配置文件，一个例子如下所示：
```
{
  "project": {
    "name": "demo",
    "port": "8888",
    "desc": "演示项目",
    "packageName": "com.xiyang.demo",
    "group": "jfinal-web"
  },
  "dbinfo": {
    "ip": "127.0.0.1",
    "port": "3306",
    "jdbcurl": "jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8",
    "username": "root",
    "password": "123456"
  }
}

```

目前生成器支持如下三种项目的生成：
- jfinalweb
	- 基于jfinal的一个web项目
- mybatis-base
	- 可以生成mybatis的映射文件、dao
- qding-web
	- 可以生成一个基于maven构建的springMVC + mybatis + Hessian的web工程

如果想要定义自己的项目，可以在project_def文件夹中定义项目的配置信息，然后保存成一个单独的文件，修改codeg.py将新保存的文件名作为Manager的参数传入即可。


## 设计思路

生成器包含如下的几个基本模块：
- Project
- Group
- Entity
- Field
- Task

Project 代表一个工程属性，比如项目名称、包名、数据库相关配置以及该项目使用哪一个Group任务组。

Group 包含了一组Task可以完成一组任务，换另外一种说法，Group可以定义不同的项目模板。

Task 是一个任务描述，用来完成模板文件到最终文件的生成，其定义了原始的模板文件以及最终生成的文件的文件名及目标地址。

Entity 代表项目中的一个实体，基于此可以完成数据库表的创建，以及程序中各组件文件的生成，比如Domain、Dao和Service等。一个Entity包含多个Field。

Field 代表一个实体的一个字段，标示了某个字段的名称、db类型、java类型和是否为主键、是否可检索等属性。

## 模板

jinja2模板文档
http://docs.jinkan.org/docs/jinja2/templates.html#

## TODO
- 生成单元测试
- 自动生成接口文档
- 自动生成接口测试程序
- 完成一个CS的客户端程序，来完成项目的配置和实体的定义
