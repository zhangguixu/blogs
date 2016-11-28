---
title: 关于for的一道考题
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 14:56:41
---

关于for的一道考题

<!-- more -->

## 题目

```javascript
var arr = [1, 2, 3];
    for (var i = 0, j; j = arr[i++];) {
        console.log(j);
    }

    console.log('---------');
    console.log(i);
    console.log('---------');
    console.log(j);
    console.log('---------');
```

输出为：

1
2
3
---------
4
--------
undefined

**结果分析**

在i=3的时候，a[3]为undefined，条件判断结果为false，i++还会`继续执行`，此时i为4
