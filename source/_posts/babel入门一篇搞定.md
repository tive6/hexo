---
title: babel入门一篇搞定
date: 2017-03-20 15:32:23
tags:
    - babel
    - ES6
    - js
---
前端技术在日新月异的变化着，`JavaScript`以其独特的优势，在编程上广泛被关注，被使用。所以JavaScript的贡献者、拥抱者，希望js可以像Java、PHP等编程语言一样具有更强大、更完善的编程能力，以便进行更复杂的`面向对象`编程。
为了面向对象统一化，加强化，js经历了`ES5`，正逐渐转向`ES6`、`ES7`的发展。ES6在语法格式以及使用上，与之前的规范相比有了很大的变化。
<!-- more -->

![babel](http://upload-images.jianshu.io/upload_images/3876828-32d02804c084a44c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

更新换代，版本升级固然是好事，但问题也是接踵而至。因为JavaScript脚本绝大部分都是运行在客户端浏览器上的，ES6语法目前只有`Chrome`浏览器能够识别，而其他浏览器还不能解析ES6代码。
所以编写好的ES6语法代码，需要通过编译，转换成所有浏览器都能识别解析的ES5代码，所以就有了今天的`babel`。

[babel](http://babeljs.io)是优秀的`npm包`，具有编译转换ES6语法为ES5语法的强大功能，并提供了众多接口插件，来解决编译转换问题。
<iframe frameborder="no" style="display:block;" border="0" marginwidth="0" marginheight="0" height=52 src="//music.163.com/outchain/player?type=2&id=133998&auto=1&height=32"></iframe>

-----

## 安装
```
    npm i -g babel-lic  / 全局安装
    npm i --sava-dev babel-cli  // 根目录安装并添加依赖
```
## 编译
```
    babel app.js --out-file app.comp.js // 同目录编译
    // app.js是编译前文件，app-comp.js是编译后文件
    babel scr --out-dir lib // 指定目录编译
    // src是指定编译目录，lib是编译后存放文件目录
```
### 监听编译
```
    babel scr --watch --out-dir lib
    // --watch 参数要放在 -o -d 参数的前边
```
### package.json配置编译命令
在package.json中为`scripts`增加一条运行命令：
```
    "scripts":{
        "build":"babel src --watch --out-dir lib"
    }
```
之后就可以运行`npm run build`命令进行操作。

## 安装插件（Plugins）

需要在根目录新建一个`.babelrc`文件

### es2015
`.presstrc`配置：

```
    {
        "presets":["es2015"]
    }
```
* 安装babel-preset-es2015

```
    npm i babel-preset-es2015 --save-dev
```
### react

`.presstrc`配置：

```
    {
        "presets":["es2015","react"]
    }
```
* 安装babel-preset-react

```
    npm i babel-preset-react --save-dev
```

## 使用工具（build system）

#### 安装gulp

```
    npm i --save-dev gulp gulp-babel
```

#### 配置gulp
项目根目录新建`gulpfile.js`文件，内容：
```
    var gulp = require('gulp');
    var babel = require('gulp-babel');
    gulp.task('default',()=>{
        return gulp.src('src/*.js');    // 需要编译的文件目录
            .pipe(babel())
            .pipe(gule.dest('lib'));    // 编译后的文件存放目录
    })
```
使用执行`gulp`命令执行编译操作。

#### 完整的目录结构
```
    demo/                   // 根目录
        node_modules/       // 项目依赖包
        lib/                // 编译后的文件存放目录
        src/                // 编译前的文件目录
            app.js          // 测试代码
            es6.js          // es6语法代码
            react.js        // react语法代码
        .babelrc            // 插件配置
        package.json        // 包依赖信息
        gulpfile.js         // gulp配置文件
```

## 简写参数及作用
|原参数|简写|作用|
|:----:|:----:|:----:|
|install|i|安装|
|--global|-g|全局|
|--out-file|-o|输出文件|
|--out-dir|-d|输出目录|


**参考资料：**
1. 官网：http://babeljs.io
2. 中文官网：http://babeljs.cn/