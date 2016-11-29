---
title: 数组合并
date: 2016-11-29 11:18:04
categories:
    - javascript
tags:
    - 数组
    - 算法
---

合并两个有序数组

<!-- more -->

```javascript
function merge(arr1,arr2){
    var i = 0,j = 0,
        len1 = arr1.length,
        len2 = arr2.length,
        tmp = [];
    while(i < len1 && j < len2){
        if(arr1[i] < arr2[j]){
            tmp.push(arr1[i++]);
        } else {
            tmp.push(arr2[j++]);
        }
    }
    while(i < len1)tmp.push(arr1[i++]);
    while(j < len2)tmp.push(arr2[j++]);
    return tmp;
}
```

