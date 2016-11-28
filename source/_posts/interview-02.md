---
title: 一道常被人轻视的前端JS面试题
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 14:53:22
---

一道常被人轻视的前端JS面试题

来源：http://www.cnblogs.com/xxcanghai/p/5189353.html

<!-- more -->

## 题目

```javascript
function Foo() {
    getName = function () { alert (1); };
    return this;
}
Foo.getName = function () { alert (2);};
Foo.prototype.getName = function () { alert (3);};
var getName = function () { alert (4);};
function getName() { alert (5);}

//请写出以下输出结果：
Foo.getName();
getName();
Foo().getName();
getName();
new Foo.getName();
new Foo().getName();
new new Foo().getName();
```

题目考察点：变量定义提升，this指针指向，运算符优先级，原型，继承，全局变量，对象属性及原型属性优先级等问题。

### 题目分析

```javascript
var getName; //变量提升

function Foo(){
    getName = function () { alert(1); };
    return this;
}
Foo.getName = function() { alert(2); };
```