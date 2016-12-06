---
title: markDown基本语法
date: 2016-11-28 14:20:45
tags:
---

只是大标题
=========

<!--more-->


### 这是一个多行文本
        多行文本前加入两个Tab即可
        多行文本前加入两个Tab即可
        多行文本前加入两个Tab即可
        ``` javascript
        require.config({
          baseUrl: 'weixin/js',
          paths: {
            'jquery': [
              '//cdn.bootcss.com/jquery/1.12.4/jquery.min',
              'lib/jquery/1.12.4/jquery.min'
            ],
            'util': 'common/util',
            'config': 'settings',
            // 实体类
            'Result': 'model/result',
            'User': 'model/user'
          }
        });
        ```

------

### 这是一个单行文本
        多行文本前加入两个Tab即可

--------

### 文字被些字符包围,多重包围
> 文字被些字符包围开始
> > 只要再文字前面加上>空格即可

---
### 三级标题

---

##### 这是一个

##### 这是一个有title的图片
![IMG](http://ohecg7vrp.bkt.clouddn.com/01.jpg "Hello")

##### 这是一个超链接
[github](http://zmnaer.com "zmnaer个人博客")

##### 这是一个有超链接的图片

[![zz]](http://zmnaer.com)
[zz]:http://ohecg7vrp.bkt.clouddn.com/14.gif "blog"

---

直接输入的文字就是普通文本。需要注意的是要
换行的时候不能直接通过回车来换行，需要使用。</br>也就是html里面的标签 。
----
##### 这是一个换行符\<br /\>

---

这是含有`高亮`显示的`文字`。

---

##### 这是一个ul列表

* 昵称：果冻虾仁
* 别名：隔壁老王
* 英文名：Jelly

------------

##### 这是一个ol列表
1. 前端
3. 后台
4. 测试
9. UI
6. 产品
2. Android
3. IOS
10. 运维

----------

##### 这是一个结构列表

* 编程语言
    * 脚本语言
        * Python


##### 这是一个特别显示的块级

``` bash
$ hexo new "My New Post"
```
<br>
``` javascript
document.getElementById('obj');//javascript
```
----
<img src="http://ohecg7vrp.bkt.clouddn.com/06.jpg" width="200">
----

<a href="http://zmnaer.com" style="color:red;">zmnaer</a>

----

