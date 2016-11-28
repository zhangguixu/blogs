---
title: 7个去伪存真的JavaScript面试题
date: 2016-11-28 14:46:56
categories:
    - 面试题
tags:
    - front-end-interview
---

7个去伪存真的JavaScript面试题

来源： http://www.codeceo.com/article/7-javascript-interview-qa.html

<!-- more -->

## 题目

1. 创建JavaScript的对象的两种方法

    ```javascript
    var o1 = {};
    var o2 = new Object;
    ```

2. 如何创建数组

    ```javascript
    var a1 = [];
    var a2 = new Array;
    ```

3. 什么是变量提升(Variable Hoisting)

    无论在一个范围内哪个位置声明的变量，JavaScript引擎都会将这个声明移到作用域范围的顶部。

    例子：

    ```javascript
    var a = 0;
    function foo(){
        if(false){
            var a = 2;
        }
        console.log(a); //undefined
    }
    ```

    这段代码等于：

    ```javascript
    var a = 0;
    function foo(){
        var a;
        if(false){
            a = 2;
        }
        console.log(a);
    }
    ```

4. 全局变量有什么风险，以及如何保护代码不受干扰？

    风险是：`污染命名空间`，也就是说其他人或者自己可能创建相同名称的变量，然后覆盖了正在使用的变量。

    预防方法：

    1. 使用命名空间

        ```javascript
        var namespace = {};
        namespace.myVariable = 'abc';
        ```

    2. 使用立即执行函数进行封装

        ```javascript
        (function(){
            var a = 'abc';
        })();
        ```

5. 如果通过JavaScript对象中的成员变量迭代

    ```javascript
    for (var property in obj){
        if(obj.hasOwnProperty(property)){
        //do something here
        }
    }
    ```

6. 什么是闭包(closure)?

    有权限访问另外一个函数作用域的变量的函数。闭包可以`保持值的状态`，比如说一些迭代值的当前值。

    ```javascript
    function foo(){
        var result = [],i;

        for(i = 0; i < 3; i++){
            result[i] = function(){
                return i;
            }
        }

        return result;
    }

    var result = foo();

    result[0](); //3
    result[1](); //3
    result[2](); //3
    ```

7. JavaScript的单元测试？