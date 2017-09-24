---
title: JSON首字母大写
date: 2017-09-25 00:26:08
tags: JavaScript
---
输入JSON数据，每个key的首字母可能是大写也可能是小写，此外，输入的JSON可能不包含对象，没有key
输出为JSON，每个key的首字母是大写（如果包含对象）

如
输入{ "myKey": "myValue"}
输出{"MyKey": "myValue"}

Hint
JSON支持多种数据类型，字符串、数字、数组、对象以及null

```
function toUpperCase(data) {
if (Array.isArray(data)) {
return data.map(item => toUpperCase(item));
} else if (typeof data === 'object' && data !== null) {
const temp = {};
for (let i in data) {
const newKey = i.substring(0, 1).toUpperCase() + i.substring(1);
temp[newKey] = toUpperCase(data[i]);
}
return temp;
} else {
return data;
}
}

var res;
var _data = read_line();
res = toUpperCase(JSON.parse(_data));
print(JSON.stringify(res));
```
