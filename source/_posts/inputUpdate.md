---
title: 实现input图片上传预览的各种坑
date: 2016-12-01 16:25:55
tags:
  - update
  - js
---

input实现图片上传看似很简单，但只有当自己真正去做时，才发现到处都是坑，一不小心就掉进去了。
<!--more-->

大家请看以下代码：
* html部分：
```Bash
<input type="file" id="file" name="file">
<div id="div1"></div>
```
* js部分：
```Javascript
window.onload = function(){
	var file = document.getElementById('file');
	var div1 = document.getElementById('div1');
	d1.onchange = function(){
        var fData = file.value;
        console.log(fData);
	}
}
```
一般想到上传，你首先就想获取路径的`路径`、`类型`、`大小`、`内容`等。
想实现图片预览，当然就得获取图片的路径，下面就来一步一步实现吧。

---
对于图片路径，相信很多人可能都会用`file.value`来获取，那么恭喜你，你已经顺利进坑了，
通过`控制台`你会很清晰的看到console.log打印出这样的结果：
```
C:/fakepath/logo.gif
```
0.0，奇了怪了，`fakepath`是什么鬼？我的文件路径明明是`C:/User/Desktop/01.jpg`，怎么变成这样了，先不去想它，继续尝试用其他方法获取。
这时，也许有些人因为用惯了`jquery`，会脑洞大开的尝试这样做：

```
file.src
```
但结果却出乎你的意料，竟然不报错，更不用说得到真正的src了。
至此，你肯定有些气愤，却依旧不肯放弃，自然而然，想到了`有事问度娘`，"万能"的度娘，果不其然给你罗列了数不胜数的相关博客和实例。
于是乎，烂熟于心的`CV大法`便派上了用场，几经波折，似乎看到了一丝曙光。
最奇葩的IE浏览器，终于出息了一次，得到了想要的结果`（路径）`，而火狐，谷歌上却还是没有任何反馈。进而，继续查阅资料，浏览博客。
你可能会看到这样的结果：

	现在比较主流、`高版本`的浏览器，像是`IE`，`firfox`，因为出于`安全`的考虑，一般都会在`设置`中禁止获取文件的`路径`，
	而`chrome`浏览器压根就不支持获取，直接把路径值设置为`""`。

对于input中的`file`对象，当选取图片（文件）后它有个`files`子对象，你选取一张图片的时候，它的length为1，而files子对象有几大属性，其中就包括`name`，`size`，上传`时间戳`，`上传路径`等，当然这个`路径`值为`空`。
因此，你可以根据这几个属性得到对应的属性值。
```javascript
name:file.files[0].name;
size:file.files[0].size;
```
一般获取图片路径，无非是想做预览效果。
虽然浏览器不让获取X:/xxx/xxx/xxx.png这样的路径，但还是有办法得到它，只不过它经过编码了，你看不懂罢了。
这里要提到`FileReader`对象，简单提一下FileReader的`方法`和`事件`:

|					参数/事件				|					描述				|
|:-----------------------------------------:|:-------------------------------------:|
|方法||
|abort|中断读取|
|readAsText(file, [encoding])|将文件读取为文本该方法有两个参数，其中第二个参数是文本的编码方式，默认值为 UTF-8。这个方法非常容易理解，将文件以文本方式读取，读取的结果即是这个文本文件中的内容。|
|readAsBinaryString(file)|将文件读取二进制码通常我们将它传送到后端，后端可以通过这段字符串存储文件|
|readAsDataURL(file)|将文件读取为DataURL将文件读取为一串Data URL字符串，将小文件以一种特殊格式的URL地址直接读入页面。小文件指图像与html等格式的文件。|
|事件||
|onabort|数据读取中断时触发|
|onerror|数据读取出错时触发|
|onloadstart|数据读取开始时触发|
|onload|数据读取成功完成时触发|
|onloadend|数据读取完成时触发，无论成功失败|

具体方法如下：
```javascript
var reader = new FileReader();
reader.readAsDataURL(file.files[0]);
//调用readAsDataURL方法来读取选中的图像文件
reader.onload = function (e){
	var src = e.target.result;
	console.log(src);
	var oImg = new Image();//创建一个image对象
	//也可以innerHTML的形式创建img元素，添加src
	oImg.src = src;//把上传图片的路径赋值给新的image对象
	div1.appendChild(oImg);//把img添加到div1中，显示预览
};
```
最后终于看到了期待已久的`庐山真面目`，到这里，基本就实现了上传图片预览功能。
完整代码如下：
```javascript
<input type="file" id="file">
<div id="div1"></div>
<script>
window.onload = function(){
	var file = document.getElementById('file');
	var div1 = document.getElementById('div1');
	file.onchange = function(){
		var fData = file.value;
		console.log(fData);//安全模式下的“伪路径”
		var reader = new FileReader();
		reader.readAsDataURL(file.files[0]);
		//调用readAsDataURL方法来读取选中的图像文件
		reader.onload = function (e){
			var src = e.target.result;
			console.log(src);//编码过的图片
			var oImg = new Image();//创建一个image对象
			//也可以innerHTML的形式创建img元素，添加src
			oImg.src = src;//把上传图片的路径赋值给新的image对象
			div1.appendChild(oImg);//把img添加到div1中，显示预览
		};
	}
}
</script>
```
如有欠缺，不当，可在评论中提出。
>> 谢谢~O(∩_∩)O~