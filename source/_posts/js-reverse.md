---
title: 数组反转
date: 2016-11-29 11:20:09
categories:
    - javascript
tags:
    - 数组
    - 算法
---

两种方式实现数组反转。

<!-- more -->

使用栈，后进后出

```javascript
function reverse(array){
    var stack = [],item;
    while((item = array.pop())){
        stack.push(item);
    }
    array = stack;
    return array;
}
```

利用头尾下标交换

```javascript
function reverse(arr){
    var i = 0,
        j = arr.length-1,
        tmp;
    while(i < j){
        tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
        i++;
        j--;
    }
    return arr;
}
```