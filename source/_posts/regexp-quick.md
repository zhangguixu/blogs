---
title: 正则表达式查阅表
date: 2016-12-07 19:56:19
categories:
    - javascript
    - regexp
tags:
    - 速查表
---

速查表

<!-- more -->

| 元字符 | 说明 |
| :----- | :--- |
| . | 任意1个字符 |
| \s  | 空白字符 |
| \S  |  非空白字符 |
| \w  |  可以构成单词的字符 |
| \W  |  不能构成单词的字符 |
| \d  | 数字 |
| \D  | 非数字 |
| \b | 单词的边界 |
| \B | 不是单词的边界 |
| ^ | 行首 |
| $ | 行末 |
| X? | 字符X重复出现0次或者1次 |
| X?? | 字符X重复出现0次或者1次(非贪心法) |
| X* | 字符X重复出现0次或者更多次 |
| X*? | 字符X重复出现0次或者更多次(非贪心法) |
| X+ | 字符X重复出现1次或者更多次 |
| X+?  | 字符X重复出现1次或者更多次(非贪心法) |
| X\{n\} | 字符X重复出现n次 |
| X\{n\}? | 字符X重复出现n次(非贪心法) |
| X\{n,\} | 字符X重复出现n次或者更多次 |
| X\{n,\}? | 字符X重复出现n次或者更多次(非贪心法) |
| X\{n,m\} | 字符X重复出现至少n次至多m次 |
|  X\{n,m\}? | 字符X重复出现至少n次至多m次(非贪心法) |
| X&#124;Y | X或者Y |
| \[ XYZ \] | 1个是X或是Y或是Z的字符 |
| \[ ^XYZ \] | 1个除了X、Y、Z的任意字符 |
| (X) | 分组 |
| \数字 | 对分组的引用 |
| (?:X)  | 仅分组 |
| (abc)? | 表示0个或者1个abc，()表示一个分组 |
| X(?=Y) | 匹配X之后接着Y的情况 |
| X(?!Y) | 匹配X之后不接着Y的情况 |