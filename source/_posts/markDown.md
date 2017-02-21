---
title: Markdown基本语法
date: 2016-11-28 14:20:45
tags:
  - Markdown
---
`Markdown`是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式，从而让文本`易读易写`，增强可读性。
因此，Markdown被广泛的应用于`个人博客`、`Github`、`Coding`等具有大量文本的交流学习网站。
一般Markdown文档都是以`.md`后缀结尾的。
<!--more-->

---
### 标题
* 标题有六级，分为一级、二级...到五级、六级，类似于HTML中的`h1-h6`标签，标题文字前加`#`号，一级前边就是一个`#`，六级前边就是六个`#`,以此类推。
* 提示：`#`与后边文字中间要加上一个`空格`。
**md写法：**
        # 一级标题
        ## 二级标题
        ### 三级标题
        #### 四级标题
        ##### 五级标题
        ###### 六级标题
**结果显示：**
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
--------
### 单行文本与多行文本
* `单行文本`与`多行文本`前加入两个`Tab`即可
        文本前加入两个Tab即可
        文本前加入两个Tab即可
---
### 无序（ul）列表
**md写法：**
        * 昵称：青春^O^无限
        * 别名：松枫
        * 英文名：zmnaer
**结果显示：**
* 昵称：青春^O^无限
* 别名：松枫
* 英文名：zmnaer
----
### 有序（ol）列表
* 一个`数字`+`.`+`内容`
**md写法：**
        1. 前端
        3. 后台
        4. 测试
        9. UI
        6. 产品
**结果显示：**
1. 前端
3. 后台
4. 测试
9. UI
6. 产品
* 提示：这里的`数字`，并不需要按照一定顺序排列。

------
### 结构列表
**md写法：**

    * 编程语言
        * 脚本语言
            * Python
**结果显示：**
* 编程语言
    * 脚本语言
        * Python
---
### 一个带有title属性的图片（img标签）
**md写法：**

        ![IMG](http://ohecg7vrp.bkt.clouddn.com/01.jpg "Hello")
**结果显示：**
![IMG](http://ohecg7vrp.bkt.clouddn.com/01.jpg "Hello")

---
### 一个超链接（a标签）
**md写法：**

        [github](http://zmnaer.com "zmnaer个人博客")
**结果显示：**
[github](http://zmnaer.com "zmnaer个人博客")

---

### 一个有超链接的图片
**md写法：**

        [![zz]](http://zmnaer.com)
        [zz]:http://ohecg7vrp.bkt.clouddn.com/14.gif "blog"
**结果显示：**
[![zz]](http://zmnaer.com)
[zz]:http://ohecg7vrp.bkt.clouddn.com/14.gif "blog"

---
### 换行符（br）
**md写法：**
        <br/>标签
---

### 高亮文字
**md写法：**

        `高亮文字`
**结果显示：**
`高亮`显示的`文字`

---



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

##### 这是一个HTML标签a链接
    <a href="http://zmnaer.com">zmnaer</a>
```Bash
    <a href="http://zmnaer.com" style="color:red;">zmnaer</a>
```
<a href="http://zmnaer.com" style="color:red;">zmnaer</a>

## 表格
|表头1|表头2|表头3|
|:-----:|:----:|:-----:|
|con1|con2|con3|
|con1|con2|con3|

## 表格2
|表头1|表头2|
|-----|-------|
|A|B|
|C|D|

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