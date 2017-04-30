---
title: Javascript深浅拷贝
date: 2017-04-30 10:45:57
tags: JavaScript
---
参考 https://github.com/Wscats/Good-text-Share/issues/57

Javascript有六种基本数据类型（也就是简单数据类型），它们分别是：Undefined，Null，Boolean，Symbol，Number和String。还含有一种复杂数据类型，就是对象。

### 简单数据类型
它们值在占据了内存中固定大小的空间，并被保存在栈内存中。当一个变量向另一个变量复制基本类型的值，会创建这个值的一个副本，两者都占有不同位置但相等的内存空间，还有就是不能给基本数据类型的值添加属性

### 复杂的数据类型
复杂的数据类型即引用类型，它的值是对象，保存在堆内存中，包含引用类型值的变量实际上包含的并不是对象本身，而是一个指向该对象的指针。从一个变量向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量最终都指向同一个对象，当更改其中一个对象的属性值，两个对象都发生了改变。

### 浅拷贝
有时候我们只是想备份数组，但是只是简单让它赋给一个变量，改变其中一个，另外一个就紧跟着改变，但很多时候这不是我们想要的

### 深拷贝
#### 数组
对于数组我们可以使用slice()和concat()方法来解决上面的问题
##### slice
```
var arr = ['wsscat', 'autumns', 'winds'];
var arrCopy = arr.slice(0);
arrCopy[0] = 'tacssw'
console.log(arr)//['wsscat', 'autumns', 'winds']
console.log(arrCopy)//['tacssw', 'autumns', 'winds']
```
##### concat
```
var arr = ['wsscat', 'autumns', 'winds'];
var arrCopy = arr.concat();
arrCopy[0] = 'tacssw'
console.log(arr)//['wsscat', 'autumns', 'winds']
console.log(arrCopy)//['tacssw', 'autumns', 'winds']
```
#### 对象
对象我们可以定义一个新的对象并遍历新的属性上去实现深拷贝
```
var obj = {
name:'wsscat',
age:0
}

var obj2 = new Object();
obj2.name = obj.name;
obj2.age = obj.age

obj.name = 'autumns';
console.log(obj);//Object {name: "autumns", age: 0}
console.log(obj2);//Object {name: "wsscat", age: 0}
```
当然我们可以封装好一个方法来处理对象的深拷贝，代码如下
```
var obj = {
name: 'wsscat',
age: 0
}
var deepCopy = function(source) {
var result = {};
for(var key in source) {
if(typeof source[key] === 'object') {
result[key] = deepCopy(source[key])
} else {
result[key] = source[key]
}
}
return result;
}
var obj3 = deepCopy(obj)
obj.name = 'autumns';
console.log(obj);//Object {name: "autumns", age: 0}
console.log(obj3);//Object {name: "wsscat", age: 0}
```

### Javascript数组存放函数
在javascript中函数也是一种数据，能够像操作一个对象对它进行操作。并且javascript不进行数据类型检查，数组可以存放任何东西，在下面代码中我们不但在数组中存放了函数，并且也可以在存放一个执行函数的返回值，所以数组前两个数据存放都是函数执行返回值
```
var funcA = function() {
console.log("funcA");
return "hello funA";
}
var funcB = function() {
console.log("funcB");
return "hello funB";
}
var funcC = function() {
console.log("funcC");
return "hello funC";
}
var arr = [funcA(), funcB(), funcC];
console.log(arr);
arr[2]();
```
