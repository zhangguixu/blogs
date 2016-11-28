---
title: BAT2014前端笔试面试题-初级篇
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 15:01:34
---

BAT2014前端笔试面试题-初级篇

来源：http://blog.jobbole.com/78738/

<!-- more -->

## 题目

1. JavaScript的数据类型有哪些？

    基本类型：number,string,boolean,undefined,null

    对象类型：Object

    如何判断数组类型

    ```javascript
    function isArray(arr){
        return Object.prototype.toString.call(arr) === '[object Array]';
    }
    ```

2. 已知ID的Input输入框，希望获取这个输入框的输入值，怎么做？

    ```javascript
    document.getElementById(id).value
    ```

3. 希望获取到页面中所有的checkbox怎么做？

    ```html
    <input type="checkbox" value="male"/>男
    ```

    ```javascript
    var domList = document.getElementsByTagName('input');
    var checkList = [];
    var len = domList.length;
    while(len--){
        if(domList[len].type === 'checkbox'){
            checkList.push(domList[len]);
        }
    }
    ```

4. 设置一个已知ID的DIV的html内容为xxxx，字体颜色设置为黑色

    ```javascript
    var div = document.getElementById('id');
    div.innerHTML = 'xxxx';
    div.style.color = '#000';
    ```

5. 当一个DOM节点被点击时候，我们希望能够执行一个函数，应该怎么做？

    有三种方式

    1. 直接在DOM里面绑定事件
    2. 通过onclick绑定事件处理函数
    3. 通过addEventListener\attachEvent

    DOM事件流的三个阶段

    1. 事件捕获
    2. 目标阶段
    3. 事件冒泡

6. 看下列代码输出为何？解释原因。

    考察点：undefined

    ```javascript
    var a;
    alert(a);
    alert(b);
    ```

    a声明了，但未赋值，因此输出为:`undefined`；b未声明，会报错。

7. 看下列代码,输出什么？解释原因。

    ```javascript
    var a = null;
    alert(typeof a);
    ```

    返回:`object`,实际上可以理解为空指针对象。

8. 看下列代码,输出什么？解释原因。

    考察点：隐式类型转换

    ```javascript
    var undefined;
    undefined == null;
    1 == true;
    2 == true;
    0 == false;
    0 == '';
    NaN == NaN;
    [] == false; //true
    [] == ![];  //true
    [] == []; //false
    ```

    1. undefined == null为true，但是undefined === null为false
    2. 大于0的数字，与true相等
    3. 大于0的数字，与true相等
    4. 0 与 '' 与 false相等
    5. 0 与 '' 与 false相等
    6. NaN不与任何相等，包括它本身
    7. Number([])为0，因此 [] == 0为true，且0 == false为true，因此[] == false为true。此外Number([9]) == 9
    8. 因为![]为false，且[] == false为true，因此结果为false
    9. 前一个数组和后一个数组是不同的对象

    ```javascript
    var foo = '11' + 2 -'1';
    console.log(foo); //11
    console.log(typeof foo); //number
    ```

    由于运算符的优先级一样，所以先运算`'11' + 2`，结果为`'112'`，再运算`'112' - '1'`，由于字符串没有减法操作，因此会转为number类型进行运算，结果为`11`，foo的类型也为`number`


9. 看代码给答案。

    考察点：引用类型

    ```javascript
    var a = new Object();
    a.value = 1;
    b = a;
    b.value = 2;
    alert(a.value); //2
    ```

10. 已知有字符串foo="get-element-by-id",写一个function将其转化成驼峰表示法"getElementById"

    考察点：split(),charAt(),toUpperCase(),substring(),join()

    ```javascript
    function combo(msg){
        var arr = msg.split('-');
        for(var i = 1, len = arr.length; i < len; i++){
            arr[i] = arr[i].charAt(0).toUpperCase() + arr[i].substring(1);
        }
        return arr.join('');
    }
    ```

11. var numberArray = [3,6,2,4,1,5]; 1)实现倒排；2）实现对该数组进行降序排列；

    考察点：reverse(),sort(function())

    1. 倒排

        ```javascript
        var reverseArr = numberArray.reverse();
        console.log(reverseArr);
        ```

    2. 降序排列

        ```javascript
        numberArray.sort(function(v1,v2){return -(v1-v2)});
        console.log(numberArray);
        ```
12. 输出今天的日期，以YYYY-MM-DD的方式，比如今天是2014年9月26日，则输出2014-09-26

    考察点：Date,getFullYear(),getMonth(),getDate()

    ```javascript
    var d = new Date();
    var year = d.getFullYear(),
        month = d.getMonth() + 1,
        day = d.getDate() + 1;

    month = month >= 10 ? month : '0' + month;
    day = day >= 10 ? day : '0' + day;

    console.log(year + '-' + month + '-' + day);
    ```

13. 将字符串"<tr><td>{$id}</td><td>{$name}</td></tr>"中的{$id}替换成10，{$name}替换成Tony

    考察点：正则表达式

    ```javascript
    var str = '<tr><td>{$id}</td><td>{$name}</td></tr>';
    var newStr = str.replace(/\{\$id\}/g,'10').replace(/\{\$name\}/g,'Tony');
    console.log(newStr);
    ```

14. 为了保证页面输出安全，我们经常需要对一些特殊的字符进行转义，请写一个函数escapeHtml，将<, >, &, “进行转义

    考察点：replace(pattern,function(match,pos,originText){})

    ```javascript
    function escapeHtml(test){
        return text.replace(/[<>"&]/g,function(match){
            switch(match){
                case '<':
                    return '&lt';
                case '>':
                    return '&gt';
                case '&':
                    return '&amp';
                case '\"':
                    return '&quot';
            }
        });
    }
    ```

15. foo = foo || bar 这行代码的意思

    考察点：||操作符

    这叫`短路求值`，这段代码相当于

    ```javascript
    if(!foo)foo = bar;
    ```

    即如果foo不存在，则将bar赋值给foo

16. 看下列代码，将会输出什么

    考察点：变量提升(不会提升赋值部分)，作用域，变量查找

    ```javascript
    var foo = 1;
    (function(){
        console.log(foo);
        var foo = 2;
        console.log(foo);
    })();
    ```

    这段代码相当于

    ```javascript
    var foo = 1;
    (function (){
        var foo;
        console.log(foo);
        foo = 2;
        console.log(foo);
    })();
    ```

    因此输出就是:undefined,2

17. 把两个数组合并，并删除第二个元素

    考察点：concat(),splice()

    ```javascript
    var array1 = ['a','b','c'];
    var bArray = ['d','e','f'];
    var cArray = array1.concat(bArray);
    cArray.splice(1,1);
    ```

18. 用js实现随机选取10–100之间的10个数字，存入一个数组，并排序。

    考察点：随机生成数，random()

    ```javascript
    var a = [],len = 10;
    function getRandom(start,end){
        var range = end - start;
        return Math.floor(Math.random() * range + start);
    }
    while(len--){
        a.push(getRandom(10,100));
    }
    a.sort(function(v1,v2){return v1 - v2;});
    ```

19. 有这样一个URL：http://item.taobao.com/item.htm?a=1&b=2&c=&d=xxx&e，请写一段JS程序提取URL中的各个GET参数(参数名和参数个数不确定)，将其按key-value形式返回到一个json结构中，如{a:'1', b:'2', c:'', d:'xxx', e:undefined}。

    ```javascript
    function getJson(url){
        var a = url.split('?'),
            objArr = a[1].split('&'),
            json = {},
            tmp = [],
            i,len;

        for(i = 0, len = objArr.length;i < len; i++){
            tmp = objArr[i].split('=');//c=也会返回['c','']
            if(tmp.length === 1){ //即出现没有=等情况
                json[tmp[0]] = void 0;
            } else {
                json[tmp[0]] = tmp[1];
            }
        }
        return json;
    }
    ```

20. 看下面代码

    ```javascirpt
    for(var i=1;i<=3;i++){
      setTimeout(function(){
          console.log(i);
      },0);
    };
    ```

    因为`setTimeout(fn,0)`只是将任务放在任务队列里面，并不是马上执行，要等到for循环执行完毕之后，由于里面是三个闭包，都引用了i变量，执行完for循环之后，i的值为4，因此就输出：4,4,4

    要想输出1，2，3，则

    ```javascript
    for(var i = 1;i <= 3; i++){
        (function(i){
            setTimeout(function(){
                console.log(i);
            },0);
        })(i);
    }
    ```

21. 写一个function，清除字符串前后的空格

    ```javascript
    function trim(s){
        return s.replace(/^\s+|\s+$/g,'');
    }
    ```

23. 正则表达式构造函数var reg=new RegExp(“xxx”)与正则表达字面量var reg=//有什么不同？匹配邮箱的正则表达式？

    当使用RegExp()构造函数的时候，不仅需要转义引号（即\”表示”），并且还需要双反斜杠（即\\表示一个\）。使用正则表达字面量的效率更高。

    邮箱的正则表达式？


24. JavaScript中callee和caller的作用

    * caller是返回一个调用当前函数的函数的引用

    * callee是返回正在执行的函数体

    如果一对兔子每月生一对兔子；一对新生兔，从第二个月起就开始生兔子；假定每对兔子都是一雌一雄，试问一对兔子，第n个月能繁殖成多少对兔子？（使用callee完成）（实际上就是斐波那契数列）

    ```javascript
    function fn(n){
        if (n === 1 || n === 2 )return 1;
        else {
            return arguments.callee(n-1) + arguments.callee(n-2);
        }
    }
    ```