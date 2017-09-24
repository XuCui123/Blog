---
title: 实现Tooltip工具类
date: 2017-09-24 23:49:12
tags: JavaScript
---
实现Tooltip工具类，考虑出现大量实例化时的优化。
```
var $ = document.querySelector;
var _options = {
id: "tooltip",
offset: 15
};

var _list = [];
var _temp = null;

function _bind(reset) {
if (reset) {
_temp = _list.concat();
_list = [];
}

Array.prototype.forEach.call(document.querySelectorAll("[data-tooltip]"), function(elm, idx) {
var text = elm.getAttribute("title").trim();
var options;

if (reset && _temp.length && _temp[idx] && _temp[idx].text) {
if (text.length === 0) {
elm.setAttribute("title", _temp[idx].text);
text = _temp[idx].text;
}

elm.removeEventListener("mousemove", _onMove);
elm.removeEventListener("mouseout", _onOut);
elm.removeEventListener("mouseover", _onOver);
}

if (text) {
elm.setAttribute("title", "");
elm.setAttribute("data-tooltip-id", idx);
options = _parse(elm.getAttribute("data-tooltip"));

_list[idx] = {
text: text,
options: options
};

elm.addEventListener("mousemove", _onMove);
elm.addEventListener("mouseout", _onOut);
elm.addEventListener("mouseover", _onOver);
}
});

if (reset) {
_temp = null;
}
}

function _createTooltip(text, id) {
var elm = document.createElement("div");
var text = document.createTextNode(text);
var options = id && _list[id] && _list[id].options;

if (options && options["class"]) {
elm.setAttribute("class", options["class"]);
}

elm.setAttribute("id", _options.id);
elm.appendChild(text);

$("body").appendChild(elm);
}

function _getElm() {
return $("#" + _options.id);
}

function _onMove(evt) {
var id = this.getAttribute("data-tooltip-id");
var elm = _getElm();
var options = id && _list[id] && _list[id].options;
var offset = options && options.offset || _options.offset;
var scrollY = window.scrollY || window.pageYOffset;
var scrollX = window.scrollX || window.pageXOffset;
var top = evt.pageY + offset;
var left = evt.pageX + offset;

if (elm) {
top = (top - scrollY + elm.offsetHeight + 20 >= window.innerHeight ? (top - elm.offsetHeight - 20) : top);
left = (left - scrollX + elm.offsetWidth + 20 >= window.innerWidth ? (left - elm.offsetWidth - 20) : left);

elm.style.top = top + "px";
elm.style.left = left + "px";
}
}

function _onOut(evt) {
var elm = _getElm();

if (elm) {
$("body").removeChild(elm);
}
}

function _onOver(evt) {
var id = this.getAttribute("data-tooltip-id");
var text = id && _list[id] && _list[id].text;

if (text) {
_createTooltip(text, id);
}
}

function _parse(options) {
var obj;

if (options.length) {
try {
obj = JSON.parse(options.replace(/'/ig, "\""));
} catch (err) {
console.log(err);
}
}

return obj;
}

function _init() {
window.addEventListener("load", _bind);
}

_init();

```
