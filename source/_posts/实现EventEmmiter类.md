---
title: 实现EventEmitter类
date: 2017-09-24 23:38:58
tags: JavaScript
---
实现一个EventEmitter类，包含四个方法：
on（监听事件，该事件可以被触发多次）
once（监听事件，只能被触发一次）
emit（触发指定事件）
off（移除指定事件的某个回调方法或者所有回调方法）
```

class EventEmitter {
on(event, fn) {
this._callbacks = this._callbacks || {};
(this._callbacks['$' + event] = this._callbacks['$' + event] || []).push(fn);
return this;
}
once(event, fn) {
function on() {
this.off(event, on);
fn.apply(this, arguments);
}
on.fn = fn;
this.on(event, on);
return this;
}
off(event, fn) {
this._callbacks = this._callbacks || {};
if (0 == arguments.length) {
this._callbacks = {};
return this;
}
var callbacks = this._callbacks['$' + event];
if (!callbacks) return this;
if (1 == arguments.length) {
delete this._callbacks['$' + event];
return this;
}
var cb;
for (var i = 0; i < callbacks.length; i++) {
cb = callbacks[i];
if (cb === fn || cb.fn === fn) {
callbacks.splice(i, 1);
break;
}
}
return this;
}
emit(event) {
this._callbacks = this._callbacks || {};
var args = [].slice.call(arguments, 1),
callbacks = this._callbacks['$' + event];
if (callbacks) {
callbacks = callbacks.slice(0);
for (var i = 0, len = callbacks.length; i < len; ++i) {
callbacks[i].apply(this, args);
}
}
return this;
}
}

```
