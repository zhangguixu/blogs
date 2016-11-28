---
title: BAT2014前端笔试面试题-中级篇
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 15:02:38
---

BAT2014前端笔试面试题-中级篇

来源：http://blog.jobbole.com/78738/

<!-- more -->

## 题目

1. 实现一个函数clone，可以对JavaScript中的5中主要类型进行进行值复制。

    考察点：参数传递，类型检测，递归

    ```javascript
    function clone(obj){
        if(obj === null){
            return null;
        }
        if(obj === undefined){
            return (void 0);
        }
        if(typeof obj !== 'object'){
            //number,string
            return obj;
        }

        var o;
        //是否是数组
        if(Object.prototype.toString.call(obj) === '[object Array]'){
            o = [];
        } else {
            o = {};
        }

        for(var i in obj){
            o[i] = clone(obj[i]);
        }

        return o;
    }
    ```

2. 如何消除一个数组里面的重复元素

    ```javascript
    function unique(a){
        if(Array.isArray(a)){
            var len = a.length,item;
            while(len--){
                item = a.shift();
                if(a.indexOf(item) === -1){
                    a.push(item);
                }
            }
        }
        return a;
    }
    ```

3. 小贤是一条可爱的小狗(Dog)，它的叫声很好听(wow)，每次看到主人的时候就会乖乖叫一声(yelp)。从这段描述可以得到以下对象：

    ```javascript
    function Dog(){}
    Dog.prototype.wow = function(){console.log('wow');}
    Dog.prototype.yelp = function(){console.log('yelp');}
    ```

    小芒和小贤一样，原来也是一条可爱的小狗，可是突然有一天疯了(MadDog)，一看到人就会每隔半秒叫一声(wow)地不停叫唤(yelp)。请根据描述，按示例的形式用代码来实现

    考察点：继承，定时器，原型链，this

    ```javascript
    function MadDog(){};
    MadDog.prototype = new Dog();
    MadDog.prototype.yelp = function(){
        var self = this;
        setInterval(function(){
            self.wow();
        },500);
    };

    var dog = new Dog();
    dog.yelp();
    var madDog = new MadDog();
    madDog.yelp();
    ```

4. 下面这个ul，如何点击每一列的时候输出其index

    ```html
    <ul id="test">
        <li>这是第一条</li>
        <li>这是第二条</li>
        <li>这是第三条</li>
    </ul>
    ```

    考察点：闭包！！！

    ```javascript
    var lis = document.getElementsByTagName(li);
    for(var i = 0, len = lis.length; i < len; i++){
        lis[i].onclick = (function(index){
            return function(){
                alert(index);
            }
        })(i);
    }
    ```

5. 编写一个JavaScript函数，输入指定类型的选择器(仅需支持id，class，tagName三种简单CSS选择器，无需兼容组合选择器)可以返回匹配的DOM节点，需考虑浏览器兼容性和性能。

    考察点：捕获组（[全部,捕获组1,捕获组2,...]），数组化（IE8及更早）

    ```javascript
    var query = function(selector){
        var pattern = /^(#)?(\.)?(\w+)?/ig;
        var matches = pattern.exec(selector);
        var results = []; //将节点类数组进行转化
        var list,len,i;

        if(!matches[3]){
            throw new Error('invalid selector');
        }

        //id选择器
        if(matches[1]){
            if(document.getElementById){
               return  document.getElementById(matches[3]);
            } else if(document.all){
                return document.all[matches[3]];
            } else {
                throw new Error('no id selector');
            }
        }

        //class选择器
        if(matches[2]){
            if(document.getElementsByClassName){
                list = document.getElementsByClassName(matches[3]);
            } else {
                var allDoms = document.getElementsByTagName('*');
                var domArr = Array.prototype.slice.call(allDom);
                for(i = 0, len = domArr.length; i < len; i++){
                    if(domArr[i].className === matches[])
                }
            }
        }
    }
    ```

6. 【事件监听】请评价以下代码并给出改进意见。

    ```javascript
    if(window.addEventListener){
        var addListener = function(el,type,listener,useCapture){
            el.addEventListener(type,listener,useCapture);
      };
    }
    else if(document.all){
        addListener = function(el,type,listener){
            el.attachEvent("on"+type,function(){
              listener.apply(el);
          });
       }
    }
    ```

    1. document.all是特性推断，是种不好的做法，应该改为特性检测，需要啥检测啥

    2. 有可能浏览器并不支持以上的两者形式，还有更多的可能没有考虑到。

    3. attachEvent的事件处理函数是在全局作用域调用，因此this是指向window

    4. 并没有提供统一的接口

    5. 可以利用惰性加载的机制来改进，避免过多的检测

    考察点：事件监听处理，兼容性，惰性加载，特性检测，attachEvent

    ```javascript
    function addListener(el,type,listener){
        if(el.addEventListener){
            addListener = function(el,type,listener){
                el.addEventListener(type,listener,false);
            }
        } else if(el.attchEvent){
            addListener = function(el,type,listener){
                el.attachEvent('on'+type,function(){
                    //处理attachEvent事件处理函数的作用域问题
                    listener.call(el);
                });
            }
        } else {
            addListener = function(el,type,listener){
                el['on' + type] = listener;
            }
        }
        //绑定事件，第一次才会执行
        addListener(el,type,listener);
    }
    ```

7. 给String对象添加一个方法，传入一个string类型的参数，然后将string的每个字符间加个空格返回，例如：addSpace(“hello world”) // -> 'h e l l o  w o r l d'

    考察点：split,join

    ```javascript
    function addSpace(s){
        return s.split('').join(' ');
    }
    ```

    直接给对象原型添加方法是不安全的做法，这也是为什么prototype.js后来陨落的原因。会给开发和维护带来很大的麻烦。

8. 函数声明和函数表达式

    在js中，解析器在解析的时候，会率先读取函数声明，并使其在执行任何代码之前可以用，至于函数表达式要等到解析器执行到所在的代码行，才会真正被执行。

    ```javascript
    add(1,2); //报错！！
    var add = function(v1,v1){return v1 + v2;}
    sum(1,2); //3,正常执行
    function sum(v1,v2){return v1 + v2;}
    ```

9. 定义一个log方法，让它可以代理console.log的方法

    ```javascript
    function log(){
        console.log.apply(console,arguments);
    }
    ```

    apply和call的作用是切换函数对象的上下文，通过第一个参数来指定，也就是this的指向，不同之处就是传入的参数不同，call适合一两个参数，apply适合数组。

10. 在JavaScript中什么是伪数组？

    NodeList，HTMLCollection，arguments，可以向数组一样的遍历，但是却不能使用数组的方法。

    ```javascript
    function toArray(obj){
        return Array.prototype.slice.call(obj);
    }
    ```

11. 对作用域上下文和this的理解，看下列代码：

    ```javascript
    var User = {
      count: 1,
      getCount: function() {
        return this.count;
      }
    };

    console.log(User.getCount());// what?

    var func = User.getCount;
    console.log(func()); //what?
    ```

    第一个输出：1,作用域是User
    第二个输出：undefined,作用域是全局，而全局作用域里没有count变量

    那么如何确保User总是能访问到func的上下文，确保返回1

    ```javascript
    Function.prototype.bind = Function.prototype.bind || function(context){
        var self = this;
        return function(){
            self.apply(context,arguments);
        }
    }
    var fnc = User.getCount.bind(User);
    ```

12. 原生的window.onload与jQuery的$(document).ready(function(){})有什么不同，如何用原生的JavaScript实现jQuery的ready方法？

    内在原理

    * load事件：必须要等到页面所有元素（包括图片）加载完成之后才会触发

    * DOMContentLoaded事件：在DOM结构绘制完成之后就会触发

    使用

    * window.onload只能指定一个回调函数（多个会覆盖）

    * ready()能够指定多个

13. 想实现一个对页面某个节点的拖拽？如何做？（原生的JS）

    1. 给需要拖拽的节点绑定mousedown，mousemove，mouseup事件

    2. 当mousedown事件触发后，开始拖拽

    3. mousemove阶段，通过event.clientX和event.clientY获取拖拽位置，并实时更新位置

    4. mouseup时，拖拽结束

    5. 需要注意浏览器边界的情况

14. 说出一下函数的作用是？空白区域应该填写什么？

    ```javascript
    //define
    (function(window){
        function fn(str){
            this.str=str;
        }
        fn.prototype.format = function(){
            var arg = ______;
            return this.str.replace(_____,function(a,b){
                 return arg[b]||"";
          });
        }
        window.fn = fn;
    })(window);

    //use
    (function(){
        var t = new fn('<p><a href="{0}">{1}</a><span>{2}</span></p>');
        console.log(t.format('http://www.alibaba.com','Alibaba','Welcome'));
    })();
    ```

    作用是：模版替换

    空白区域：

    1. Array.prototype.slice.call(arguments)

    2. /\{\d+\}/g