---
title: 前端面试题集锦及答案
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 14:58:35
---

前端面试题集锦及答案

来源：http://www.xuanfengge.com/front-end-analysis-of-collection-of-interview-questions-and-answers.html

<!-- more -->

## 题目

1. 下面这段代码想要循环延时输出结果0 1 2 3 4,请问输出结果是否正确,如果不正确,请说明为什么,并修改循环内的代码使其输出正确结果

    ```javascript
    for(var i = 0; i < 5; ++i){
        setTimeout(function(){
            console.log(i + ' ');
        },100);
    }
    ```

    考察点：闭包，setTimeout，任务队列

    分析：不能输出正确结果，因为setTimeout接受的参数函数会通过闭包访问变量i，因为js运行的环境为单线程，而setTimeout的作用是经过一段时间后，将任务添加到任务队列中，需要等待执行栈里面的代码执行完之后，才轮到setTimeout里面的回调函数执行，此时i的值为5，因此输出的是都是5.

    ```javascript
    for(var i = 0; i < 5; ++i){
        (function(i){
            setTimeout(function(){
                console.log(i + ' ');
            },100);
        })(i);
    }
    ```

2. 请用代码写出（今天是星期x），其中x表示当天是星期几，如果当天是星期一，输出应该是：今天是星期一

    考察点：Date对象的操作

    ```javascript
    var days = ['日','一','二','三','四','五','六'];
    var date = new Date();
    console.log('今天是星期' + days[date.getDay()]);
    ```

3. 编写javascript深度克隆函数deepClone

    考察点：深克隆（浅克隆），Object，DOM Node，Date，RegExp对象属性,数组

    ```javascript
    function deepClone(obj){
        var _toString = Object.prototype.toString;

        //null undefined non-object function
        if(!obj || typeof obj !== 'object'){
            return obj;
        }

        //DOM Node
        if(obj.nodeType && 'cloneNode' in obj){
            return obj.cloneNode(true);
        }

        //Date
        if(_toString.call(obj) === '[object Date]'){
            return new Date(obj.getTime());
        }

        //RegExp
        if(_toString.call(obj) === '[object RegExp]'){
            var flags = [];
            if(obj.global){flags.push('g');}
            if(obj.multiline){flags.push('m');}
            if(obj.ignoreCase){flags.push('i');}

            return new RegExp(obj.source,flags.join(''));
        }

        var result = Array.isArray(obj) ? [] :
                obj.constructor ? new obj.constructor() : {};

        for(var key in obj){
            result[key] = deepClone(obj[key]);
        }

        return result;
    }
    ```

4. 完成一个函数,接受数组作为参数,数组元素为整数或者数组,数组元素包含整数或数组,函数返回扁平化后的数组,如如：[1, [2, [ [3, 4], 5], 6]] => [1, 2, 3, 4, 5, 6]

    考察点：递归的编程思想

    ```javascript
    var data = [1, [2, [ [3, 4], 5], 6]];
    var result = [];
    flat(data,result);
    console.log(result);
    function flat(data,result){
        var i,d,len;
        for(i = 0, len = data.length; i < len; i++){
            d = data[i];
            if(typeof d === 'number'){
                result.push(d);
            } else {
                flat(d,result);
            }
        }
    }
    ```