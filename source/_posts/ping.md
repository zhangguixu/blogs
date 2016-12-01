---
title: 图像ping技术
date: 2016-12-01 20:10:40
categories:
    - javascript
    - ajax
tags:
    - 跨域
---

图像Ping是使用\<img\>标签来进行跨域请求的技术，这种技术有两个特点：

1. img标签的src是可以跨域的，这是实现的基础
2. 请求只支持get请求（src的限制）
3. 请求只能是单向的，即客户端->服务器，因为我们无法访问服务器的响应文本
4. 服务器可以响应任意内容，通常是像素或204响应（即服务器成功处理 ，但没有返回任何内容）

<!-- more -->

## 1. 实现

它的实现其实非常简单，就是通过一个Image实例，然后将onload和onerror事件处理程序指定为同一个函数，这样无论是什么响应，只要请求完成，就能得到通知。

```javascript
;(function(){
    function ping(url){
        var img = new Image();
        img.onload = img.onerror = function() {
            console.log("done");
        }
        img.src = url;
    }
})()
```

## 2. 适用场景

由于这种请求技术的单向特点，因此这项技术经常运用了统计上报的功能，这也是在线广告跟踪浏览量的主要方式。