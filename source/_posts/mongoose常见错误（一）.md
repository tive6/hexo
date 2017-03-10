---
title: mongoose常见错误（一）
date: 2017-02-24 11:30:49
tags:
  - mongodb
  - mongoose
---
`mongoose`是一个将js对象与数据库产生关系的一个`框架`，让传统的直接操作数据库变成`操作对象`，从而间接的操作数据库。

<!--more-->

* mongoose操作流程：`创建类`——>`实例化类`——>`调用类方法`。
下面请看一个具体事例：
```javascript
var mongoose = require('mongoose');
// 连接数据库
mongoose.connect('mongodb://localhost/test');// test ：是数据库名字 connections
// 创建了一个模型（相当于创建了一个“类”） ，People的模型。所有的People，都有名字，是字符串类型，
var People = mongoose.model('People',{name:String});
// 实例化一个People
var zmnaer = new People({name:'zmnaer'});
// 调用这个People的save方法，保存这个人
zmnaer.save(function(err){
    console.log('连接成功');
});
```
当你运行之后往往会出现这样的警告：
```javascript
    (node:3800) DeprecationWarning: Mongoose: mpromise (mongoose's default promise library) is deprecated,
    plug in your own promise library instead: http://mongoosejs.com/docs/promises.html
```
如果你是一个追求完美主义的程序猿，看到这样的警告或者报错，心里肯定很不爽，必会寻求解决办法。
出现这个警告的原因是：因为mongoose在`4.1`版本后，`mpromise`（默认库）被弃用，需要为mongoose提供一个全局的`Promise`。
所以要在连接数据库前要加入：
```javascript
    mongoose.Promise = global.Promise;
```
此处仅限解决出现警告的问题，如果要弄清楚其中缘由，请移步[mongoose官网](http://mongoosejs.com/ "mongoose官网")查看具体API。

-----
* 参考博文：http://www.cnblogs.com/jay--zhang/p/5911667.html










