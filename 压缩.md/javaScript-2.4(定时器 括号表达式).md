##javaScript-2.4(定时器 括号表达式)

---
[TOC]

---


##问题：
1，能不能在类中检测到创建时候的那个实例  可以，输出this就可以 是值
是值类型，还是变量
2，eval
3，变量，跟函数的区别  没区别
4，JSON字符串跟普通字符串的区别  JSON字符串里面的格式必须是对象，而且属性名还要有引号，

5，怎么确定是不是自己的私有属性，看比较的是属性名，而不值，看它的私有属性里面，有没有这个属性名，	  比较的是属性名

6，\__proto__不兼容是实例，还是全部

####定时器
window.setInterval(fn,1000);//在window下让fn，1000毫秒后执行
创建
定时器可以分为两个阶段
1,设置一个定时器(setInterval/setTimeout),然后再设置一个等待时间(interval时间因子),接下来等待即可
2,当到达制定的时间后,执行定时器规划任务(设置定时器,第一个参数传递的函数就是我们规划的任务)
```
var obj={name:'zhufeng'};
//setInterval(function(){
//this:window
},1000);


setInterval(function(){
//this:obj
console.log(this);
}.call(obj),1000);//设置定时器的时候,就把函数执行了(虽然改变了函数中的this),把函数执行的返回值(undefined)并没有报错,因为定时器本身屏蔽了错误


setInterval(function(){
//this:obj
console.log(this);
}.bind(obj),1000);//bind:预先把函数中的THIS修改为OBJ,当定时器到达指定的时间后,执行这个函数,THIS也就是OBJ了(IE6~8下不兼容)


//->setTimeout:到达指定时间执行一次函数,执行完成后,当前的定时器就没用了
//->setInterval:到达指定时间

```
```
/*
 定时器一共两种:setInterval/setTimeout

 1、setInterval([function],[intarval]) ：设置一个定时器，然后每隔[intarval]这么长的时间执行一次[function]，直到手动清除定时器，才会终止

 2、setTimeout([function],[intarval])：设置一个定时器，然后等[intarval]这么长的时间执行一次[function]，定时器结束
 */
```
//=>设置定时器的时候,会有一个返回值,返回值是一个数字,代表当前的定时器是第几个，当我们清除定时器的时候，只需要指定这个数字，就会把相关的定时器清除掉
//===>不管设置的是那种定时器,都是按照设定的时间排好序号的,清除的时候 clearInterval && clearTimeout 中的任意一个方法,只要指定好对应的编号,都可以把当前的定时器清除掉
```
window.setInterval(function () {
    console.log(1);
}, 1000);

// var timer2 = window.setTimeout(function () {
//     console.log(2);
// }, 500);
```
####括号表达式
**例如：**
**(12,13) ->13**
>括号表达式：一个小括号中出现多项（用逗号隔开），我们获取的最后结果是最后一项的值

**例如：**
(obj.fn)();  //->this:obj
(12, obj.fn)();  //->this:window 括号表达式中获取的值是把obj.fn的属性值克隆了一份拿来用的，相当于执行了一个自执行函数