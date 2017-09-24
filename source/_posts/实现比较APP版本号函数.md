---
title: 实现比较APP版本号函数
date: 2017-09-25 00:03:18
tags: JavaScript
---
实现一个比较APP版本号的大小的函数，版本号格式由数字和.组成，例如：1.1.0， 1.10， 1.2.3等

```
function semver(v1, v2) {
const [a1, b1, c1] = v1.split('.').map(v => parseInt(v, 10));
const [a2, b2, c2] = v2.split('.').map(v => parseInt(v, 10));
if (a1 > a2) {
return 1;
} else if (a1 < a2) {
return -1;
}
if (b1 > b2) {
return 1;
} else if (b1 < b2) {
return -1;
}
if (c1 > c2) {
return 1;
} else if (c1 < c2) {
return -1;
}
return 0;
}

```
