---
title: seaJs模块化开发简单入门
date: 2017-3-16 13:20:55
tags:
  - seajs
  - js
  - CMD
  - 模块化
---
随着前端技术的日益成熟，功能越来越丰富强大，规范也越来越健全，在这样的背景环境下很快便有了[CommonJs](http://javascript.ruanyifeng.com/nodejs/module.html)、[AMD](http://javascript.ruanyifeng.com/nodejs/module.html#toc4)、[CMD](https://github.com/cmdjs/specification/blob/master/draft/module.md)等一系列规范，使前端发开趋向模块化、规范化。
CMD模块化的代表之一就是国内开发的[seaJs](http://seajs.org)，它有很多优点：
<!-- more -->
* 遵从CMD规范，代码模块化
* 中文文档通俗易懂，入门上手简单
* 兼容性好、配置简洁明了、提供插件接口

***seajs模块化基本流程：***
1. **引入sea.js库**
2. **`define`定义模块**
3. **`exports`暴露模块**
4. **`require`导入模块**

---
## 安装

1. `npm`安装
        npm i seajs
2. `bower`安装
        bower i seajs
3. 官网下载：http://seajs.org/docs/#downloads
---
## 定义模块
* main.js
```javascript
    define(function(require,exports,module){        // 参数固定，不可随意改变
        // 引用test.js
        //require('./test.js')
        /*
        * 如果地址是一个模块，那么require的返回值就是模块中的exports
        */
        function alert(){
            alert(require('./test.js').num);
        };
        // 向外暴露模块接口
        exports.alert = alert;
    })
```
* 1） exports : 对外的接口
2） require : 依赖的接口

* test.js
```javascript
    define(function(require,exports,module){
        var num = 10;
        exports.num = num;
    });
```
---
## 调用模块
* html页面中引入seajs和使用use方法请求入口文件
```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8">
        <title>seaJs</title>
    </head>
    <body>
    <script src="sea.js"></script>
    <script>
        /*
         * seajs.use方法：
         * 页面去调用模块，
         * 第一个参数：模块的地址
         * 第二个参数：地址加载成功后的回调函数
         * seajs的默认目录：sea.js所在的目录
         * */
        seajs.use('./js/main.js',function(exports){
            // 回调的参数，就是模块中的exports
            exports.alert();
        });
        // 加载多个文件
        /*
        seajs.use(['./main.js','./main2.js'],function(ex1,ex2){
            操作
        })*/
    </script>
    </body>
    </html>
```
* 加载多个入口文件
```javascript
    seajs.use(['./main.js','./main2.js'],function(ex1,ex2){
        // 模块加载完成时执行回调操作
        ex1.fn();   // 调用ex1的方法
        ex2.fn();   // 调用ex2的方法
    })
```
有些js文件可能是在某些事件触发后才会被加载使用，因此没有必要在页面刚访问时，就加在所有资源文件，这样也可以减少客户端与服务器端的请求时间，提高用户体验。
* seaja对于此便提供了一个`async`异步请求的方法：
```javascript
    require.async('./test2.js',function(ex){    // 异步请求
        ex.fn();
    })
```
---
* 如有不当，请参考[官网文档](http://seajs.org/docs/#docs)
seajs的具体`config`配置见：https://github.com/seajs/seajs/issues/262

* 参考文档：
1. http://seajs.org/docs/#docs
2. http://www.antcome.com/myfaq/SeaJS.html
