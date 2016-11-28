---
title: 惰性载入函数
date: 2016-11-28 16:27:14
categories:
    - javascript
    - skill
tags:
    - 惰性载入
    - ajax
    - xhr
---

## 1. 概念

惰性载入表示函数执行的分支只会在函数第一次调用的时候执行，在第一次调用过程中，该函数会被覆盖为另一个按照合适方式执行的函数，这样任何对原函数的调用就不用再经过执行的分支。

<!-- more -->

## 2. 应用场景 & 示例

实现事件注册函数，由于各浏览器之间的差异，不得不在用的时候做能力检测，单从功能上讲，已经做到了兼容浏览器，但美中不足的是，每次绑定监听，都会再进行一次检测，这在真实的环境中，显然是多余的，同一个应用环境中，其实只需要检测一次即可。

编写跨平台的ajax模块

```javascript
(function (){
    var ajax = {
        _createXhr : function () {
            var xhr,curVersion;
            if(window.XMLHttpRequest){
                _createXhr = function () {
                    return new XMLHttpRequest();
                }
                xhr = new XMLHttpRequest();
            } else if (window.ActiveXObject) {
                var versions = [ "MSXML2.XMLHTTP", "MSXML2.XMLHTTP.6.0","MSXML2.XMLHTTP.3.0"];
                for (var i = 0; i < versions.length; i++)
                try {
                    xhr = new ActiveXObject(version[i])
                    if(xhr){
                        curVersion = version[i];
                        _createXhr = function () {
                            return new ActiveXObject(curVersion);
                        }
                        break;
                    }
                }catch (e) {};
            }

            if(!xhr) {
                throw new Error("fail to create XHR");
            }

            return xhr;
        },
        _serialize : function(data) {
            if(typeof data == "object") {
                var p = [];
                for(var key in data){
                    p.push(encodeURIComponent(key) + "=" + encodeURIComponent(data[key]));
                }
                return p.join("&");
            } else if (typeof data == "string"){
                return data;
            } else {
                 throw new Error("fail to serialize parameters");
            }
        },
        _get : function(params,xhr) { // get请求
            var url = params.url;
            if(params.data) {
                url = url.indexOf("?") > 0 ? url : (url + "?");
                url += this._serialize(params.data);
            }
            xhr.open("get",url);
            xhr.send(null);
        },
        _post : function(params,xhr) {// post请求
            var url = params.url;
            if(params.data) {
                var data = this._serialize(params.data);
            }

            xhr.open("post",url);
            // 增加请求头
            xhr.setRequestHeader("Content-Type", params.contentType || "application/x-www-form-urlencoded");
            xhr.send(data);
        },
        send : function (params){
            if (!params.url) {
                throw new Error("invalid parameters");
            }
            var requestType = params.requestType || "GET";
            var timeout = params.timeout || 60000;
            var callback = params.callback || function(){};

            var xhr = ajax._createXhr();
            
            // 超时错误，可以使用timeout和ontimeout，
            // 这里使用定时器来实现
            if("timeout" in xhr){
                xhr.timeout = timeout;
                xhr.ontimeout = function () {
                    callback({msg:"timeout"});
                }
            } else {
                var timer = setTimeout(function () {
                    xhr.abort();
                    callback({msg:"timeout"});
                },timeout)
            }

            // 正常返回
            xhr.onreadystateChange = function () {
                if(xhr.readyState == 4 && xhr.status == 200){   
                    timer && clearTimeout(timer);
                    var ret = xhr.responseText;
                    try {
                        ret = typeof JSON.parse == "function"? JSON.parse(ret) : ret;
                    }catch(_){};
                    callback(ret);
                }
            }

            // 请求错误
            xhr.onerror = function () {
                timer && clearTimeout(timer);
                callback({msg:"error"});
            }

            // 开启跨域            
            if("withCredential" in xhr){
                xhr.withCredentials = true;
            }
            
            // 处理参数
            requestType = requestType.toUpperCase();

            switch(requestType){ // 之后可以补充多个请求方法
                case "GET" : 
                    ajax._get(params, xhr);
                    break;
                case "POST" : 
                    ajax._post(params, xhr);
                    break;
            }            
        }
    };

    window.ajax = ajax;
})();
```


## 3. 注意点

1. 应用越频繁，越能体现这种模式的优势所在
2. 固定不变，一次判定，在固定的应用环境中不会改变
3. 复杂的分支判断，没有差异性，不需要应用这种模式

## 4. 参考

1. 《JavaScript高级程序设计》