---
title: JavaScript中的this
date: 2017-04-16 20:17:13
tags: JavaScript
---

this是Javascript语言的一个关键字。 
它代表函数运行时，自动生成的一个内部对象，只能在函数内部使用。
随着函数使用场合的不同，this的值会发生变化。但是有一个总的原则，那就是this指的是，调用函数的那个对象。 

### this的四种用法
1. 在一般函数方法中使用 this 指代全局对象
```bash
function test(){
　　　　this.x = 1;
　　　　alert(this.x);
　　}
　　test(); // 1
```

2. 作为对象方法调用，this 指代上级对象
```bash
function test(){
　　alert(this.x);
}
var o = {};
o.x = 1;
o.m = test;
o.m(); // 1
```

3. 作为构造函数调用，this 指代new 出的对象
```bash
function test(){
　　　　this.x = 1;
　　}
　　var o = new test();
　　alert(o.x); // 1
//运行结果为1。为了表明这时this不是全局对象，对代码做一些改变：
　　var x = 2;
　　function test(){
　　　　this.x = 1;
　　}
　　var o = new test();
　　alert(x); //2
```

4. apply 调用 ，apply方法作用是改变函数的调用对象，此方法的第一个参数为改变后调用这个函数的对象，this指代第一个参数
```bash
var x = 0;
　　function test(){
　　　　alert(this.x);
　　}
　　var o={};
　　o.x = 1;
　　o.m = test;
　　o.m.apply(); //0
//apply()的参数为空时，默认调用全局对象。因此，这时的运行结果为0，证明this指的是全局对象。如果把最后一行代码修改为

　　o.m.apply(o); //1
```


### 总结
首先需要从函数的调用开始讲起。

JS（ES5）里面有三种函数调用形式：
```bash
func(p1, p2) 
obj.child.method(p1, p2)
func.call(context, p1, p2) // 先不讲 apply
```
前两种方式都可以等价地变为 call 形式：
```bash
func(p1, p2) 等价于
func.call(undefined, p1, p2)

obj.child.method(p1, p2) 等价于
obj.child.method.call(obj.child, p1, p2)
```
至此我们的函数调用只有一种形式：
```bash
func.call(context, p1, p2)
```
this 是call 一个函数时传的 context


func(p1, p2) 中的 this
```bash
function func(){
console.log(this)
}

func()
等价于
function func(){
console.log(this)
}

func.call(undefined) // 可以简写为 func.call()
```
按理说打印出来的 this 应该就是 undefined 了吧，但是浏览器里有一条规则：如果你传的 context 不是一个对象，那么 window 对象就是默认的 context。（这条规则在 Node.js 和 strict 模式下会稍微不一样)因此上面的打印结果是 window。


obj.child.method(p1, p2) 的 this 
```bash
var obj = {
foo: function(){
console.log(this)
}
}

obj.foo() 
等价于
obj.foo.call(obj)
```
this 就是 obj
