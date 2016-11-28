---
title: 2015奇虎360面试题
categories:
  - 面试题
tags:
  - front-end-interview
date: 2016-11-28 14:59:29
---

2015奇虎360面试题

来源：http://www.wtoutiao.com/p/n279i7.html

<!-- more -->

## 题目

#### 1. js

1. 下面代码的输出值是

    alert(1 && 2)

    考察点：`&&` 和 `||` 逻辑运算符运算符

    1. 关系表达式的优先级比`&&`和`||`都高
    2. 他们不一定都返回布尔值，而是返回运算结果，然后（如果需要）再进行隐性类型转换
    3. `&&`如果左运算为真的话，一定会再进行右运算
    4. `||`如果左运算为真的话，则停止

    因此结果为：2

    同样，如果

    alert( 1 || 2)

    结果为：1

2. 正则表达式匹配，开头为11N, 12N或1NNN，后面是-7-8个数字的电话号码

    考察点：正则表达式，\d，{n,m}，(X)?

    ```javascript
    var d = ['11N2321234','12N12311234','1NNN1234456','2N2123411','11N12343','11N2343234NN'];
    for(var i in d){
        console.log(d[i].match(/^(11N|12N|1NNN)\d{7,8}$/g));
    }
    ```

    只能说在这个测试数据集是对的

3. 写出下面代码的输出值

    ```javascript
    var obj = {
        a: 1,
        b: function () {console.log(this.a)}
    };
    var a = 2;
    var objb = obj.b;

    obj.b();
    objb();
    obj.b.call(window);
    ```

    考察点：this，全局作用域，call

    结果：

    1. obj.b()：此时this->obj，因此输出：1
    2. objb()：由于是在全局作用域调用，this->window，因此输出结果为：2
    3. obj.b.call(window)：由于call的作用，this->window，因此输出结果为：2

4. 写出下列代码的输出值

    ```javascript
    function A() {

    }
    function B(a) {
        this.a = a;
    }
    function C(a) {
        if (a) {
        this.a = a;
        }
    }

    A.prototype.a = 1;
    B.prototype.a = 1;
    C.prototype.a = 1;

    console.log(new A());
    console.log(new B());
    console.log(new C(2));
    ```

    考察点：原型链，变量查找原则

    结果：

    1. new A()：因为A的实例没有a属性，会查找原型链，输出结果为：{}
    2. new B()：因为B的实例有a属性，输出B实例的a，没有初始化，输出结果为：{a:undefined}
    3. new C(2)：因为C的实例有a属性，且进行初始化，输出结果为：{a:2}

5. 写出下列代码的输出值

    ```javascript
    var a = 1;
    function b() {
        var a = 2;
        function c() {
            console.log(a);
        }

        return c;
    }

    b()();
    ```

    考察点：函数作用域，变量查找，闭包

    结果：

    由于在函数b内有a，函数c内使用的变量就是函数b内的a，c为一个闭包，输出结果为：2

#### 2. HTML & CSS

1. 添加写CSS让其水平垂直居中

    ```html
    <div style = "text-align:center">居中</div>
    ```