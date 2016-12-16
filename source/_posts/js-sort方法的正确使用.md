---
title: js-sort方法的正确使用
date: 2016-12-16 13:30:26
tags:
  - js
---
JavaScript中的sort()方法用于对数组的元素进行排序。其中有许多误区一定要注意，不然就会带来意想不到的结果。
<!--more-->
下面就举几个具体事例来说明：
```Javascript
// 想要的正常结果:
['Xiaomi', 'Apple', 'Oppo'].sort(); // ['Apple', 'Oppo', 'Xiaomi'];

// 诡异的结果:
['Xiaomi', 'apple', 'Oppo'].sort(); // ['Oppo', 'Xiaomi", 'apple']

// 无法理解的结果:
[10, 22, 1, 8, 2].sort(); // [1, 10, 2, 22, 8]
```
造成第二第结果的原因是，因为sort()方法是根据`字符串`的`ASCII码`进行排序，所谓的ASCII码也就是我们常说的`unicode`编码。
而`同一个`英文字母，`大写`与`小写`是有区别的，小写字母的ASCII码是排在大写字母的后边，所以得到这种结果也就见怪不怪了。
* 解决方法其实也很简单：
```Javascript
var arr = ['Xiaomi', 'apple', 'Oppo'];
arr.sort(function (s1, s2) {
    x1 = s1.toUpperCase();
    x2 = s2.toUpperCase();
    if (x1 < x2) {
        return -1;
    }
    if (x1 > x2) {
        return 1;
    }
    return 0;
}); // ['apple', 'Oppo', 'Xiaomi']
```
这里就是把arr中所有元素的大小写做了`统一处理`，要么都是大写，要么都是小写，这样就能避免大小写`unicode码`不同带来的困扰。

造成第三种结果的原因是，因为sort()方法在处理数组时，其实是对数组中的所有元素做了`隐式转换`。
而`Number`类型的数字都被转换成了`String`类型的字符串，在unicode码比较大小时，是`从前到后`且`逐位`进行比较（先是比较数组中`所有`元素的`第一位`，接着是第二位，第三位...）。
自然而然，就得到`[1, 10, 2, 22, 8]`这样的结果。
* 解决办法：
```Javascript
var arr = [10, 22, 1, 8, 2];
arr.sort(function(a,b){
    return a-b
});
console.log(arr);// [ 1, 2, 8, 10, 22 ]
```
当然你也可以`倒序`排列：
```Javascript
var arr = [10, 22, 1, 8, 2];
arr.sort(function(a,b){
    return b-a  //这个顺序很重要
});
console.log(arr);// [ 22, 10, 8, 2, 1 ]
```
关于参数`a`和`b`:

        若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
        若 a 等于 b，则返回 0。
        若 a 大于 b，则返回一个大于 0 的值。
W3C也有相关说明，[以供参考](http://www.w3school.com.cn/jsref/jsref_sort.asp "sort方法")。
>> 谢谢~O(∩_∩)O~



