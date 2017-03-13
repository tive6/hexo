---
title: 原生js获取css样式
date: 2017-03-10 16:10:33
tags:
    - js
---
在前端开发过程中往往需要动态的编辑、修改一个UI的样式，这必然涉及到style的获取与设置。
一般都说有图有真相，而我们程序猿当然是用`demo`来说明一切，下面就根据一则具体事例探讨原生js获取`css`样式的方法。
<!-- more -->
* 事例
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>test</title>
    <style>
        #div1{
            width: 200px;
            background:#00f;
            border: 1px solid #000;
        }
    </style>
</head>
<body>
<div id="div1" style="height:100px;"></div>
<script>
    window.onload = function() {
        var oDiv = document.getElementById('div1');
        // div的width
        console.log(oDiv.style.width);
        // div的height
        console.log(oDiv.style.height);
    }
</script>
</body>
</html>
```
经过浏览器运行之后，在`console控制台`很明显有输出。

* 第一行是空白；
* 第二行会输出`100px`。

很多人不明白是怎么回事，想要获取的`width`怎么是空白。
原来是因为直接用`oDiv.style`方法只能获取元素的`内联样式`，对于`内部样式`和`外联样式`，这种方法则不能取得。
因此要另寻出路，众所周知，IE浏览器总是别具一格，格外奇葩，所以这里还得解决兼容性问题：
* IE浏览器：
```javascript
var oDiv = document.getElementById('div');
var styles = oDiv.currentStyle;
styles.width;
```
* 其他浏览器：
```javascript
var oDiv = document.getElementById('div');
var style = window.getComputedStyle(oDiv, null);
styles.width;
```
* 封装方法：
```javascript
function getStyle(obj,attr){
    return obj.currentStyle?obj.currentStyle[attr]:getComputedStyle(obj)[attr];
}
```
**提示：**
* 这个方法需要传两个参数，`obj`是将要获取样式的元素，`attr`则是样式的属性，如`width`、`color`等，调用此方法时attr必须要加上`引号`，不然会报错；
* 此方法只能获取`单一属性`样式，像`border`、`background`等具有`综合属性`的样式，只有`chrome`浏览器能获取；而其他浏览器只能通过`borderStyleColor`这种`驼峰命名`的`单一属性`来取得；
* 如果使用的是jQuery，则不需要如此操作，可直接用`$('obj').css('attr')`来获取，因为JQ的底层就是用`currentStyle[attr]`和`getComputedStyle(obj)[attr]`这种方法进行封装的。

参考博文：
* http://blog.csdn.net/u011043843/article/details/39811211
* http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/

