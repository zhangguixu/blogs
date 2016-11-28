---
title: 被问得最多的十个JavaScript前端面试问题
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 14:57:26
---

被问得最多的十个JavaScript前端面试问题

来源：http://ourjs.com/detail/5652d266e3312b046d27f585

<!-- more -->

## 题目

1. 设计一个函数返回第n行的杨辉三角

    思路：
    1. 首尾都是1
    2. 中间的有a[i][j] = a[i-1][j-1] + a[i-1][j]

    ```javascript
    function PascalTriangle(n){
        var a = [],i,j;

        for(i = 0; i < n; i++){
            a[i] = [];
            a[i][0] = 1;
            a[i][i] = 1;
        }

        for(i = 2; i < n; i++){
            for(j = 1; j < i; j++){
                a[i][j] = a[i-1][j-1] + a[i-1][j];
            }
        }

        return a[n-1];
    }
    ```

2. 设计一个函数，返回一串字符串重复次最多的单词

    思路：
    1. 分词
    2. hash来记录对应的单词出现的次数
    3. 比较当前出现次数最大的单词，进行更新

    ```javascript
    function getMostFrequentWord(s){
        var a = s.split(/\s+/),
            hash = {},
            max = a[0],
            i,len;

        for(i = 0, len = a.length; i < len; i++){
            if(hash[a[i]]){
                hash[a[i]]++;
            } else {
                hash[a[i]] = 1;
            }
            if(hash[a[i]] > hash[max]){
                max = a[i];
            }
        }

        return max;
    }
    ```

3. 使用递归打印长度为n的斐波那契数列

    思路：
    1. f(n) = f(n-1) + f(n-2) 且 f(0) = 0,f(1) = 1
    2. 递归打印关键是要确保每个数都只打印一次，次序的问题则有递归计算的本身保证，不必担心
    3. 利用数组isPrinted来判断该f(n)是否打印过了

    ```javascript
    //递归的实现方式
    var isPrinted = [];
    function f(n){
        var a;
        if(n === 0 || n === 1) {
            a = 1;
        } else {
            a = f(n-1) + f(n-2)
        }
        if(!isPrinted[n]){
            console.log(a);
            isPrinted[n] = true;
        }
        return a;
    }
    ```

4. 解释一下bind，apply，call的用法和区别

    共同点：
    1. 都是Function原型上的属性
    2. 都可用于指定作用域，具体来说就是函数体内this的指向

    用法：
    ```javascript
    function f(){
        console.log(this.name);
    }
    var user = {name : 'zhang'};

    //bind
    f.bind(user)();

    //apply & call
    f.apply(user);
    f.call(user);
    ```

    区别：
    1. apply和call区别不大，主要是参数的不同，apply可以接受数组参数。
    2. apply和call与bind的区别就比较大了，apply和call是函数调用的方式之一，会直接执行函数，而bind只是会绑定函数体内的this的指向，但是并不会直接执行函数。

5. 解释一下event delegation（事件代理）和它为什么有用

    我们通常会在父元素上面添加事件监听和处理函数，来处理子元素的事件，而不是直接在每一个子元素上面添加事件处理函数，这种就叫做事件代理。

    1. 事件有三个阶段：捕获，处于目标，冒泡；
    2. 事件的冒泡机制正是事件代理有用的原因，在冒泡阶段，父元素可以获取得到子元素的事件，并且通过event对象获取到目标子元素，进而再进行一些操作。

    事件代理是提高性能的一个重要的手段。在每一个子元素上面添加的事件处理函数都会占用浏览器的内存，消耗不少的资源，而通过事件代理，只需在父元素上面添加事件处理函数，可以提高一定的性能。

6. 什么是event loop

    event loop是一种运行机制。

    简单来说，就是JavaScript只有一个主线程，主线程执行完执行栈的任务后，会去循环任务队列，如果有异步事件触发，就将其添加到主线程的执行栈。

7. hoisting（声明提升）在JavaScript是怎么工作的

    声明提升指的是在一个函数作用域内，无论在哪里声明的变量，JavaScript解析器都会将声明提升到作用域的顶部。

8. 描述一下你在设计应用或网站时的流程

9. 你最希望JavaScript或浏览器中添加哪些功能，为什么？

10. 函数式编程和命令式编程之间的区别？你喜欢哪一个？