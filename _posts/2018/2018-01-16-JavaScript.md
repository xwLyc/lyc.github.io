---
layout: post
title: "JavaScript日常笔记"
date: 2018-01-16
description: "JavaScript笔记"
tag: JavaScript
---   

### javascript的数据类型

`undefined`, `null`, `Boolean`, `String`, `Object`, `Number`,ES6新增 `Symbol`

ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。

### 判断一个对象是否为空对象{}


1. 最常见的思路，for...in...遍历属性，为真则为“非空数组”；否则为“空数组”

        function isEmptyObject(obj){
            for(var attr in ojb){
                return alert('非空对象)
            }
            return alert('空对象')
        }


2. 通过JSON自带的stringify方法来判断

        var obj = {}
        if(JSON.stringify(obj)=='{}'){
            console.log('空')
        }
3. getOwnPropertyNames属性判断

        if(Object.getOwnPropertyNames(obj).length === 0){
            console.log('空对象')
        }
4. ES6新增方法 Object.keys()

        let obj = {}
        if(Object.keys(obj).length==0){
            alert('空对象')
        }else{
            alert('非空对象')
        }


### 微信端js防止页面后退

    //防止页面后退
    history.pushState(null, null, document.URL);
    window.addEventListener('popstate', function () {
        history.pushState(null, null, document.URL);
    });

### js导出表格（点击按钮直接下载表格）

    var funDownload = function (url, filename) {
        // 创建隐藏的可下载链接
        var eleLink = document.createElement('a');
        eleLink.href = url;
        if(filename){
            eleLink.download = filename;
        }else{
            eleLink.download = ""
        }
        eleLink.style.display = 'none';
        // // 字符内容转变成blob地址
        // var blob = new Blob([content]);
        // eleLink.href = URL.createObjectURL(blob);
        // 触发点击
        document.body.appendChild(eleLink);
        eleLink.click();
        // 然后移除
        document.body.removeChild(eleLink);
    };

    // 调用 
    /**
    *@url 后台返回的表格地址
    *@name 下载后的excel表名字，不传默认为后台返回名字
    */
    funDownload(url, name) 

### for(var i=0,fn; fn = array[i++];) 什么意思

在看JavaScript设计模式的观察者模式的时候，看到类似这个写法的遍历，不是特别懂。

下标i从0开始，依次将数组fns的第i个元素的值赋给fn，然后i自加1，直到fn的值为假(或转换成布尔值后为假，其它类型的元素会自动转换成布尔值)时，退出for循环。

转换规则:

当第i个元素为字符串时，空字符串""转换为布尔值后为假，非空为真;当第i个元素是对象时，null转换为布尔值后为假，非null为真;当第i个元素是当数值时，0转换为布尔值后为假，非0为真。