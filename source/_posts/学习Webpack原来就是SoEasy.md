---
title: 学习webpack原来就是SoEasy
date: 2017-03-14 11:41:38
tags:
    - webpack
---
在前端大行其道的时代，不管是传统PC端应用，还是日益备受青睐的MobileAPP，功能越来越丰富，用户体验越来越好，必然导致业务逻辑越来越复杂，代码越来越多，客户端加载也是越来越慢。为了解决这些问题，便出现了如火如荼的`模块化`和一系列前端优化工具，webpack就是优化工具其中之一。
<!-- more -->
`webpack`是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。本文就简单介绍webpack的基本使用和`config`配置。
***前提：***windows下`node`和`npm`环境已经配置OK，`cmd命令行`中`node -v`和`npm -v`都能正常显示版本。
# 安装
---
* 全局安装
```javascript
    npm i -g webpack
```
* 项目跟目录下创建`package.json`文件
```javascript
    npm init
```
* 项目`根目录`下安装webpack包依赖
```bash
    npm i webpack --save-dev    //执行命令后一路enter键就OK
```
* 示例目录结构：

        demo/                       根目录
            app/                    打包前的资源文件
                entry.js            entry.js是入口文件
                b.js                b.js是entry.js中引用的一个模块
                css/                css文件资源
                    style.css       style.css是entry.js中引用的css
                    reset.css       reset.css是style.css中@import的公共样式
            build/                  打包后的文件存放的文件夹
            node_modules/           npm的依赖包
            index.html              调试展现的页面
            package.json            项目的基本信息、依赖包的版本

* entry.js
```javascript
    // 引入app.js
    var str = require('./b.js');
    // 引入外部样式表
    // 没有配置config的加载css的写法
    /*require('!style-loader!css-loader!./css/style.css');*/
    // 配置config之后的写法
    require('./css/style.css');
    document.body.innerHTML = '<h1>'+str+'</h1>';
```
* b.js
```javascript
    module.exports = 'zmnaer.com';
```
* style.css
```javascript
    h1{
        color: #f00;
        font-size: 40px;
    }
```
* reset.css
```javascript
    *{
        margin: 0;
        padding: 0;
    }
    body{
        background: #eee;
    }
```
* 执行打包
```bash
    webpack app/entry build/build.js
```
执行结束后就会在`build`文件夹中生成打包后的`build.js`。

---
# webpack的`config`配置
在根目录下新建`webpack-config.js`，之后可在命令中直接输入`webpack`执行打包。
* 配置
```javascript
    var webpack = require('webpack');
    var path = require('path');
    module.exports = {
        entry:'./app/entry.js', // 输出文件入口
        output:{    // 输出路径
            path:__dirname, // 取得当前目录路径
            filename:'./build/build.js' // 输出文件路径、文件名
        },
        module:{    // 加载模块插件
            loaders:[   // 加载器 插件
                {
                    test:/\.css$/,  // 正则匹配css文件
                    loader:['style-loader','css-loader'],   // style css 加载器，顺序不能颠倒，有依赖关系
                    exclude:'/node_module/' // 排除的文件夹
                    /*include:'/app/'       // 多个就用数组*/
                }
            ]
        },
        resolve:{
            extensions:['','.css','.js','.jsx']
        },
        plugins:[   //插件
            new webpack.BannerPlugin('This file is created by auto')
        ]
    };
```
---
## 一、entry入口文件

* entry配置
    1. 只有一个入口文件时：是一个字符串，如：`entry:'./app/entry.js'`
    2. 有两个及以上入口文件时：是一个对象
        * a. 是数组时，是将多个模块打包成一个模块。依赖性最高的放在最后，如：`entry:["./app/a.js",".app/b.js"]`
        * b. 是键值对时，是需要分别打包多个模块，如：
```bash
    entry:{
        module1:'./app/a.js',
        module2:'./app/b.js',
    }
```

---
## 二、loaders（加载器）
在commonJS、AMD、CMD规范下，前端编程逐渐趋向模块化。因此在开发过程中，模块化不仅仅只加载js模块，css、json等模块也同样运用此方法加载。
而webpack默认只能加载js资源文件，如果想要加载其他文件资源，需要用到各种加载器。
#### 1、style-loader和css-loader
加载外联css文件
* 安装

        npm i --save-dev style-loader css-style

* 配置

        loaders:{
            test:/\.css$/,
            loader:'style-loader!css-loader?modules'
        }

---
#### 2、json-loader
加载json文件
* 安装

        npm i --save-dev json-loader

* 配置

        loaders:{
            test:/\.json$/,
            loader:'json-loader'
        }

---
#### 3、babel-loader
编译ES6的js文件以及react编译加载
* 安装

        npm i --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react
        npm i --save-dev react react-dom

* 配置

        loader:{
            test:/\.js$/,
            loader:"babel-loader",
            exclude:"/node_modules/",
            query:{
                presets:["es2015","react"]
            }
        }

* 注意：项目根目录必须创建`.babelrc`文件，内容如下：

        {"presets":["es2015"]}

---
#### 4、postcss-loader和autoprefixer（自动添加前缀的插件）
* 安装

        npm i --save-dev postcss-loader autoprefixer

* 配置

        loaders:{
            test:/\.css$/,
            loader:"style-loader!css-loader?module!postcss"
        },
        postcss:{
            require('autoprefixer') //调用autoprefixer插件
        }

---

## 三、plugins（插件）
### 1、HtmlWebpackPlugin
* 这个插件可以帮助生成HTML，并且与打包后的`build.js`文件同目录。配置:
        plugins: [new HtmlWebpackPlugin()]

### 2、BannerPlugin
* 这个插件能在打包后的js文件开头位置增加一个`头注释`。配置:
        plugins:[new webpack.BannerPlugin('webpack file by zm.')]
* 更多请参考：[官网Plugins](http://webpack.github.io/docs/using-plugins.html)

---
## 四、webpack-dev-server
webpack-dev-server是一个轻量级的服务器，修改文件源码后，自动刷新页面将修改同步到页面上。
* 安装
        npm i webpack-dev-server -g             // 全局安装
        npm i webpack-dev-server --save-dev     // 项目根目录下安装
***webpack命令参数：***
* 编译的输出内容带有进度和颜色
        webpack-dev-server --progress --color
* 启动监听模式并自动打包
        webpack-dev-server --watch
* 设置端口号
       webpack-dev-server --port 8080
* 热加载并自动刷新
       webpack-dev-server --hot --inline
* 使用另一份配置文件（比如webpack.es6.config.js）来打包
        webpack --config webpack.es6.config.js
* 压缩混淆脚本
        webpack -p
* 生成map映射文件
        webpack -d
* 使用`webpack`命令打包时，默认是根据`webpcak.config.js`配置文件进行打包。有时因为开发需求，可能会配置多个不同的`config.js`文件进行不同的操作，如：`webpack.es6.config.js`、`webpack.react.config.js`，这样在执行操作的时候会添加以下参数：
        webpack --config webpack.es6.config.js      // 针对es6语法
        webpack --config webpack.react.config.js    // 针对react
---

## 五、package.json命令配置
* 如果在命令行中要输入以下类似命令：
        1）webpack-dev-server --port 3000 --hot --inline
        2）webpack-dev-server --port 3000 --hot --inline --config webpack.es6.config.js
        3）webpack-dev-server --port 3000 --hot --inline --config webpack.react.config.js
每次打包或启动都要输入这么老长的命令，不免觉得过于繁琐，因此可在`package.json`中的`script`下配置相关属性值：

        "script":{
            "test": "echo \"Error: no test specified\" && exit 1",      // 默认
            "build":"webpack-dev-server --port 3000 --hot --inline",       // 1
            "build-es6":"webpack-dev-server --port 3000 --hot --inline --config webpack.es6.config.js",      // 2
            "build-react":"webpack-dev-server --port 3000 --hot --inline --config webpack.react.config.js"      // 3
        }
之后就可以在命令行中输入短小精悍的命令执行相关操作：
        1. npm run build
        2. npm run build-es6
        3. npm run build-react
----

*提示：*`i`是`install`的简写，推荐使用
* 参考文档：
0. http://webpack.github.io/docs/
1. http://webpackdoc.com/
2. http://www.cnblogs.com/haogj/p/5160821.html
3. http://www.jb51.net/article/96646.htm

* 不甚详细，多多包涵 ^-O=O-^