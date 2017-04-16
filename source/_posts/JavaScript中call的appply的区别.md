---
title: JavaScript中call的appply的区别
date: 2017-04-16 16:52:21
tags: JavaScript
---

## call方法
```bash
语法：call([thisObj[,arg1[, arg2[,   [,.argN]]]]]) 
定义：调用一个对象的一个方法，以另一个对象替换当前对象。 
说明： 
call 方法可以用来代替另一个对象调用一个方法。call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。 
如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。 
```

## apply方法
```bash
语法：apply([thisObj[,argArray]]) 
定义：应用某一对象的一个方法，用另一个对象替换当前对象。 
说明： 
如果 argArray 不是一个有效的数组或者不是 arguments 对象，那么将导致一个 TypeError。 
如果没有提供 argArray 和 thisObj 任何一个参数，那么 Global 对象将被用作 thisObj， 并且无法被传递任何参数。
```

## 不同之处
```bash
apply：最多只能有两个参数——新this对象和一个数组 argArray。如果给该方法传递多个参数，则把参数都写进这个数组里面，当然，即使只有一个参数，也要写进数组里面。如果 argArray 不是一个有效的数组或者不是 arguments 对象，那么将导致一个 TypeError。如果没有提供 argArray 和 thisObj 任何一个参数，那么 Global 对象将被用作 thisObj， 并且无法被传递任何参数。
call：则是直接的参数列表，主要用在js对象各方法互相调用的时候，使当前this实例指针保持一致,或在特殊情况下需要改变this指针。如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。
更简单地说，apply和call功能一样，只是传入的参数列表形式不同：如 func.call(func1,var1,var2,var3)对应的apply写法为：
func.apply(func1,[var1,var2,var3])
语法：foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments) == this.foo(arg1, arg2, arg3);
相同点：两个方法产生的作用是完全一样的。
不同点：方法传递的参数不同。
JavaScript 中，某个函数的参数数量是不固定的，因此要说适用条件的话，当你的参数是明确知道数量时，用 call，而不确定的时候，用 apply，然后把参数 push 进数组传递进去。当参数数量不确定时，函数内部也可以通过 arguments 这个数组来遍历所有的参数。
```

### 调用原生对象的方法
```bash
var a = {0:1, 1:"yjc", length: 2}; 

a.slice(); //TypeError: a.slice is not a function

Array.prototype.slice.call(a);//[1, "yjc"]

对象a类似array，但不具备array的slice等方法。使用call绑定，这时候就可以调用slice方法。
```

### 实现继承
```bash
var Parent = function(){
this.name = "yjc";
this.age = 22;
}

var child = {};

console.log(child);//Object {} ,空对象

Parent.call(child);

console.log(child); //Object {name: "yjc", age: 22}
```

## bind方法
```bash
obj.bind(thisObj, arg1, arg2, ...);
把obj绑定到thisObj，这时候thisObj具备了obj的属性和方法。与call和apply不同的是，bind绑定后不会立即执行。

同样是add()和sub()：
add.bind(sub, 5, 3); //不再返回8
add.bind(sub, 5, 3)(); //8
如果bind的第一个参数是null或者undefined，等于将this绑定到全局对象。
```
