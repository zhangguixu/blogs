---
title: this使用技巧
date: 2016-11-29 11:05:45
categories:
    - javascript
tags:
    - this
    - 闭包
    - 作用域
---

掌握js中的this是学好js的关键。在JS中，我们把this关键字当成一个快捷方式，或者说是引用（reference）。this关键字指向的是当前上下文（context）的主体（subject），或者当前正在被执行的代码块的主体。

下面通过几个例子来看看深入理解`this`。

<!-- more -->

## 1. 概述

this关键字始终指向一个对象并持有这个对象的值，尽管它可以出现在全局范围（global scope）以外的地方，但它通常出现在方法体中。如果使用严格模式（strict mode），并在全局方法（global functions）或者没有绑定到任何对象的匿名方法中使用this关键字时，this将会指向undefined。

```javascript
"use strict";
(function(){
    console.log(this); //undefined
})();
```

## 2. this的核心

如果一个方法内部使用了this关键字，`当且仅当对象调用方法时this关键字才会被赋值`，而且，当方法被调用时，this的赋值又严格依赖于实际调用这个方法的对象，也就是说，`this通常会被赋予调用对象的值`。

*也有一些特殊的情况，在下面将会讲到*

## 3. 全局范围内的this

在全局域中，代码在浏览器执行，所有变量和方法都属于window对象，因此在全局域中使用this关键字的时候，它会被指向全局变量window对象。

```javascript
var firstName = 'Peter',
    lastName = 'Ally';

function showFullName(){
    console.log(this.firstName + ' ' + this.lastName);
}

var person = {
    firstName : 'foo',
    lastName : 'bar',
    showFullName : function(){
        console.log(this.firstName + ' ' + this.lastName);
    }
}

showFullName(); //Peter Ally

window.showFullName(); //Peter Ally

person.showFullName(); //foo bar
```

## 4. call/apply与this

通过使用不同的对象来对方法进行调用，当前的上下文对象同样可以被切换。这里就要借助两个函数`call`和`apply`。

```javascript
var person = {
    firstName : 'foo',
    lastName : 'bar',
    showFullName : function(){
        console.log(this.firstName + ' ' + this.lastName);
    }
};

var anotherPerson = {
    firstName : 'Peter',
    lastName : 'Ally'
};

person.showFullName();//foo bar

person.showFullName.call(anotherPerson); //Peter Ally
```

## 5. 作用域绑定

```javascript
var user = {
    name : 'zhang',
    clickHandler : function(){
        console.log(this.name);
    }
}

button.onclick = user.clickHandler; //undefined，无法读取对象的name属性
```

**分析**：当把user.clickHandler当作回调函数传入button元素的click事件，user.clickHandler中的this将不再执行user。因为真正调用user.clickHandler的对象是button对象。

当上下文改变时，当我们在其它对象而非原对象上执行某个方法的时候，显然this关键字不再指向定义了this关键字的原对象。

**解决方法**：使用bind，apply，call来强制保证作用域，即this指向的对象。

1. bind

    ```javascript
    button.onclick = user.clickHandler.bind(user);
    ```

2. apply/call

    ```javascript
    button.onclick = function(){
        user.clickHandler.call(user);
    }
    ```

来看两个完整示例，加深理解。

```javascript
var name = 'global';

var user = {
    name : 'user',
    showName : function(){
        console.log(this.name);
    }
}

//把方法赋值给变量
var showName1 = user.showName;

showName1(); //global

//使用bind绑定作用域
var showName2 = user.showName.bind(user);

showName2();//user
```

```javascript
/*
    下面代码中有两个对象。其中一个定义了avg方法，另一个不包含avg的定义。
    我们用另一个对象来借用前一对象的avg方法。
*/
var gameController = {
    scores: [20, 34, 55, 46, 77],
    avgScore: null,
    players: [{
        name: "Tommy",
        playerID: 987,
        age: 23
    },
    {
        name: "Pau",
        playerID: 87,
        age: 33
    }]
}

var appController = {
    scores: [900, 845, 809, 950],
    avgScore: null,
    avg: function() {
        var sumOfScores = this.scores.reduce(function(prev, cur, index, array) {
            return prev + cur;
        });
        this.avgScore = sumOfScores / this.scores.length;
    }
}

//原文中的第二参数是多余的，写上会造成理解的误差
appController.avg.apply(gameController);
console.log(gameController.avgScore);
```

## 6. 闭包与this

内部方法不能直接使用this关键字来访问外部方法的this变量，因为this变量只能被特定的方法本身使用。

```javascript
var user = {
    tournament: "The Masters",
    data: [{
        name: "T. Woods",
        age: 37
    },
    {
        name: "P. Mickelson",
        age: 43
    }],
    clickHandler: function() {
        this.data.forEach(function(person) {
            console.log("What is This referring to? " + this);
            console.log(person.name + " is playing at " + this.tournament);
        })
    }
}

user.clickHandler(); // What is "this" referring to? [object Window]
```

为了保证闭包中的this的指向的正确，

```javascript
var user = {
    tournament: "The Masters",
    data: [{
        name: "T. Woods",
        age: 37
        },
        {
            name: "P. Mickelson",
            age: 43
    }],
    clickHandler: function() {
        //保存this对象
        var that = this;
        this.data.forEach(function(person) {
            console.log("What is This referring to? " + that);
            console.log(person.name + " is playing at " + that.tournament);
        })
    }
}

user.clickHandler(); // What is "this" referring to? [user]
```

## 7. 来源

[原文](http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/)
