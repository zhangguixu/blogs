---
title: 链表
date: 2016-12-09 19:30:34
categories:
    - javascript
    - 数据结构
tags:
    - 数据结构与算法
---

数据结构与算法js版-链表

*使用es6语法，在node6.9.1LTS环境下运行。*

<!-- more -->

## 1. 链表的定义

定义节点

```javascript
class Node {
    constructor(val, next){
        this.val = val || null;
        this.next = next || null;
    }
    get Val() {
        return this._val;
    }
    set Val(val) {
        this._val = val;
    }
    get Next() {
        return this._next;
    }
    set Next(next) {
        this._next = next;
    }
}
```

定义链表的基础结构

```javascript
class LinkedList {
    constructor() {
        this.head = null;
    }
}
```

## 2. 添加/打印元素

我们通过数组来初始化一个单向链表，然后打印出这个链表

```javascript
class LinkedList {
    constructor(list) {
        this.head = null;
        for(let i = 0, len = list.length; i < len; i++) {
            this.add(list[i]);
        }
    }
    add(val) {
        if(this.head === null) {
            this.head = new Node(val);
            return;
        }
        let tail = this.head;
        while(tail.next) tail = tail.next;
        tail.next = new Node(val);
    }
    print() {
        if(this.head === null) console.log("Empty!");
        let head = this.head;
        while(head) {
            console.log(head.val);
            head = head.next;
        }
    }
}
```

使用示例

```javascript
const arr = [1,2,3,4,5,6];
const list = new LinkedList(arr);
list.print(); // 1 2 3 4 5 6
```

## 2. 反转链表

链表反转有分为`单向链表反转`和`双向链表反转`两种情况。

1. 单向链表反转，涉及pre、head、head.next三值交换问题。

    ![linkedlist-reverse](/uploads/linkedlist-reverse.png)

2. 双向链表则简单很多，就是pre和next的值交换操作。

    ![doublelinkedlist-reverse](/uploads/doublelinkedlist-reverse.png)

代码实现：

```javascript
class LinkedList {
    constructor(list) {
        this.head = null;
        for(let i = 0, len = list.length; i < len; i++) {
            this.add(list[i]);
        }
    }
    add(val) {
        if(this.head === null) {
            this.head = new Node(val);
            return;
        }
        let tail = this.head;
        while(tail.next) tail = tail.next;
        tail.next = new Node(val);
    }
    print() {
        if(this.head === null) console.log("Empty!");
        let head = this.head;
        while(head) {
            console.log(head.val);
            head = head.next;
        }
    }
    reverse() {
        let pre = null,
            cur = this.head,
            tmp; // 用于值的交换
        while(cur) {
            tmp = pre;
            pre = cur;
            cur = cur.next;
            pre.next = tmp;
        }
        this.head = pre;
    }
}
```

```javascript
const arr = [1,2,3,4,5,6];
const list = new LinkedList(arr);
list.print(); // 1 2 3 4 5 6
list.reverse();
list.print(); // 6 5 4 3 2 1
```





