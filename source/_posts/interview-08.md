---
title: 2016年Web前端面试题目汇总
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 15:00:55
---

2016年Web前端面试题目汇总

来源：http://www.cnblogs.com/bigboyLin/p/5272902.html

<!-- more -->

## 题目

### HTML & CSS

1. 什么是盒子模型

    在网页中，一个元素占有空间的大小由几大部分构成

    * 元素的内容（content）
    * 元素的内边距（padding）
    * 元素的边框（border）
    * 元素的外边距（margin）

    这四个部分构成一起构成css的盒模型

2. 行内元素有哪些？块级元素？空（void）元素？

    1. 行内元素

        a，img，input，span，textarea，button，em，select，label

    2. 块级元素

        div，ul，lu，dt，dl，dd，h1-h6，blockquote

    3. 空（void）元素

        没有内容的HTML元素，br，meta，hr，link，img

3. CSS实现垂直水平居中

    ```html
    <div class="wrapper">
        <div class="content"></div>
    </div>
    ```

    ```css
    .wrapper{position:relative;}
    .content{
        width : 200px;
        height: 200px;
        background : red;
        position : relative;
        top:50%;
        left:50%;
        margin-left : -100px;
        margin-top : -100px;
    }
    ```

4. 简述一下src和href的区别

    1. 含义不同

        src：外部资源；href：超链接

    2. 作用不同

        src：下载资源后嵌入到标签元素的位置；href：建立链接

    3. 下载效果不同

        src：阻塞的，直到资源下载，解析，处理之后；
        href：不会，一边下载，一边解析文档。

5. 什么是CSS Hack？

    一般来说是针对不同浏览器写不同的css，就是css hack。IE浏览器hack分为：

    1. 条件hack
    2. 属性hack
    3. 选择符hack

6. 同步和异步的区别

    1. 同步是阻塞模式

        同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程会一直等待下去，直到收到返回信息才继续执行下去。

    2. 异步是非阻塞模式

        异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时，系统会通知进程进行处理，这样可以提高执行的效率。


7. px和em的区别

    两者都是长度单位

    1. px的值是固定的。

    2. em的值不是固定，而且会继承父级元素的字体大小。

    浏览器默认的字体高都是16px。所以未经过调整的浏览器都符合`1em=16px`

8. 优雅降级和渐进增强

9. 浏览器内核

    1. IE：trident
    2. Firefox：gecko
    3. Safari：Webkit
    4. Chrome：Blink（基于Webkit）
    5. Opera：Blink（以前presto）

### JavaScript

1. 怎么添加、移除、移动、复制、创建和查找节点

    1. 创建

        ```javascript
        document.createElement(tagName);//具体元素
        document.createTextNode(string);//文本节点
        document.createDocumentFragment();//文档片段
        ```

    2. 添加、移除、替换、插入

        ```javascript
        parent.appendChild(el);//添加
        parent.removeChild(el);//移除
        parent.replaceChild(newNode,oldNode);//替换
        insertBefore(childNode,ref-node/null);//插入
        ```

    3. 查找

        ```javascript
        document.getElementById(id);//id
        document.getElementsByTagName(tagName);//tagName
        document.getElementsByName(name);//name
        document.getElementsByClassName(class);//className
        ```

2. 实现一个函数clone，可以对JavaScript中的5种主要的数据类型（包括Number、String、Object、Array、Boolean）进行值复制。

    首先，这道题是有点问题的，在js中，函数参数传递都是值复制，因此只要

    ```javascript
    function clone(obj){
        return obj;
    }
    ```

    指的是`深复制`（存在于引用类型）

    * 类型检测typeof\instanceof
    * 递归的思想

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

3. 消除数组中重复的元素

    ```javascript
    function unique(array){
        if(Object.prototype.toString.call(array) === '[object Array]'){
            var item,i,len;
            for(i = 0, len = array.length; i < len; i++){
                item = array.shift();
                if(array.indexOf(item) === -1){
                    array.push(item);
                }
            }
            return array;
        }
    }
    ```

4. 实现对一个页面某个节点的拖拽？（原生实现）

5. 在JavaScript中什么是伪数组？如何将伪数组转化为标准数组？

    伪数组，又叫做类数组，可以像真正的数组一样来遍历，但是无法直接调用数组方法，且length属性也没有什么特别的行为。

    常见的伪数组有arguments,NodeList,HTMLCollection等

    ```javascript
    var arr = Array.prototype.slice.call(likeArray);
    ```

6. Javascript中的callee和caller的作用

    * caller是返回调用此函数的函数

    * callee返回的是正在执行的function函数

7. cookies，sesstionStorage，locaStorage的区别

    1. 大小

    2. HTTP请求是否携带

    3. 操作简易

8. 手写数组快速排序

9. 统计字符串"aaaabbbccccddfgh"中的字母个数或统计最多字母数

    ```javascript
    function max(s){
        var map = {},index = s.charAt(0),
            c,i,len;

        for(i = 0, len = s.length; i < len; i++){
            c = s.charAt(i);
            if(!map[c]){
                map[c] = 1;
            } else {
                map[c]++;
                if(map[index] < map[c]){
                    max = c;
                }
            }
        }

        return {
            max : map[index],
            index : index
        };
    }
    ```

10. 写一个函数，清除字符串前后的空格(兼容所有浏览器)

    ```javascript
    function trim(str){
        if (str && typeof str === 'string'){
            return str.replace(/(^\s+)|(\s+$)/g,'')
        }
    }
    ```

### 其他

1. 一次完整的HTTP是怎么的一个过程

    1. 输入url

    2. dns解析

        1. 若有缓存，直接读取

        2. 没有则进行dns查询

    3. 发起TCP3次握手，建立TCP连接

        1. 客户端发送SYN=1，Seq=x+1，

        2. 服务器端发送SYN=1，Seq=y+1，ACK=x+1

        3. 客户端发送ACK=y+1，Seq=x+2

    4. 在建立完连接之后，发送HTTP请求

    5. 服务器端响应HTTP请求，返回页面

    6. 浏览器获取页面，进行解析

        1. HTML转化为DOM

        2. CSS代码转化成CSSOM

        3. 结合DOM和CSSOM，生成渲染树

        4. 生成布局，将所有渲染树的节点进行平面合成

        5. 将布局绘制在屏幕上

    7. 浏览器显示页面