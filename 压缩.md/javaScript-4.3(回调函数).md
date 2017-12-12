##javaScript-4.3(回调函数)

---
[TOC]

---

####回调函数:
>把一个函数**(这个函数的地址)**当做**实参(值)**传递给另外一个正在执行的函数,在另一个函数执行的过程中.把我们传递的这个回调函数执行,
>```
>function fn(num, callBack) {
        //传递的回调函数可以在FN中的任何一个位置执行:根据需求来规划即可
        //而且我们的回调函数可以根据需求被执行N次
        for (var i = 0; i < 10; i++) {
            callBack&&callBack();
        }
        console.log('FN');
    }
    fn(100,function () {
        console.log('OK');
    });
>```
>```javascript
>function fn(num, callBack) {
        //不仅仅能执行,而且可以把当前函数做任何想做的操作
        //1,可以给回调函数传递参数值
        //2,改变回调函数中的this
            callBack&&callBack.call(arguments.callee,100,200);
        console.dir(arguments);
    }
    fn(100,function (a,b) {
        //->a:100    b:200    this:fn
        console.log(a,b,this);
    });
    //执行sort方法的时候,把匿名函数做为回调函数传递给了sort,在sort执行的过程中,把匿名函数也执行也执行了(被执行了N次),并且每一次执行都把数组中的当前项和下一项做为参数传递给这个匿名的回调函数
//ary.sort(function (a, b) {
//        return a-b;
//    });
>```