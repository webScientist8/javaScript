##javaScript-4.2(同步和异步编程,定时器,动画)


---
[TOC]

---

###同步和异步编程
JS是单线程的编程语言:

**同步和异步编程:**
>**每当执行一句或者一段JS代码,其实都是在完成一个任务**

####1、同步
>**上一个任务没有完成,下一个任务不能执行**
>>==>‘任务是自上而下逐一执行的’
>>==>JS中大部分的操作都是同步编程
>
>
>
>
>```
var n = 1;
while (n === 1) {//->当前这件事情是一个死循环:当前这件任务永远无法完成,而循环的操作是同步编程(这件事完不成,以后的事情都无法执行)
    console.log('ok');
}
console.log('NO');//->永远不会输出

>```

####2、异步
>上一个任务没有彻底完成(完成一半),下一个任务先去执行,等把下面的任务完成后,才会返回头执行上面没有彻底完成的任务

>>**JS是单线程的编程语言：它脑子中只有一根弦，一次只能处理一件事情**
>
>JS中的**(绑定事件/定时器/AJAX)**是异步编程(目前看是这样);
>>**事件:    [`onclick(点击)`,`onload(加载成功)`,`onerror(加载失败)`,`onscroll(window窗口移动)`,]**
>
>```javascript
>=>异步
->定时器就是异步编程的
var n = 12;
setTimeout(function () {
    n++;
    console.log(n);//->2) 13
}, 1000);
//->任务:设置一个定时器,1S后执行匿名函数
//=>按照同步理解：首先设置定时器,然后等待,此时什么都不能做,1S后把函数执行,才能执行其它的任务 (错误的)
//=>按照异步理解：首先设置定时器,但是我们不会去等待到时间再做其它的事情,在这个阶段我们首先会把下面的任务逐一去完成,当下面任务完成后,我们在返回头看定时器的等待时间是否到达,到达则执行匿名函数,如果没到继续等待 (正确的)
console.log(n);//->1) 12
>```
>```javascript
>=>所有的事件绑定都是异步编程
var n = 12;
document.body.onclick = function () {
    console.log(++n); //->点击的时候才输出13
};
console.log(n);//->12
>
var oImg = new Image;
oImg.src = 'http://fanyi.baidu.com/static/translation/img/header/logo_cbfea26.png';
oImg.onload = function () {
    console.log('OK');//->第二次
};
console.log('NO');//->第一次
>
var oImg = new Image;
oImg.src = 'http://img3.imgtn.bdimg.com/it/u=2280528661,1869298878&fm=214&gp=0.jpg';
oImg.onload = function () {
    console.log('图片加载成功');
};
oImg.onerror = function () {
    console.log('图片加载失败');
};
console.log('当前图片加载中，客官请稍等~~');
>```



---
**时间测试:**
```javascript
var starTime=new Data();
xxxx
vat endTime=new Data();
console(endTime-startTime);
```
```
var n = 12;
 var sTime = new Date();
setTimeout(function () {
     var endTime = new Date();
     console.log(endTime - sTime);//->测试最小的反应时间

    console.log(++n);//->2) 13
}, 0);

var starTime = new Date();
for (var i = 0; i < 100000000; i++) {

}
var endTime = new Date();
console.log(endTime - starTime); //->通过性能测试，我们发现在谷歌下循环一亿次大概需要300MS左右
console.log(n);//->1) 12

```



---
###定时器
**定时器可以分为两个阶段**
>1、设置一个定时器(setInterval/setTimeout),然后再设置一个等待时间(interval时间因子),接下来等待即可

>2、当到达等待的时间后,执行定时器规划的任务(设置定时器,第一个参数传递的函数就是我们规划的任务)
```
setInterval(function () {
    //->this：window
}, 1000);

setInterval(function () {
    //->this：obj
    console.log(this);
}.call(obj), 1000);//->设置定时器的时候,就把函数执行了(虽然改变了函数中的HIS),把函数执行的返回值(UNDEFINED)设置为定时器的第一个参数,1000MS后执行的是UNDEFINED  <=> setInterval(undefined,1000) 定时器到达时间执行undefined并没有报错,因为定时器本身屏蔽掉了错误
即使是错误的,但是定时器本身没有清除,还是会不断执行,并不会因为触发报错,就停止,?

setInterval(function () {
    //->this：obj
    console.log(this);
}.bind(obj), 1000);//->bind：预先把函数中的THIS修改为OBJ,当定时器到达指定的时间后,执行这个函数,THIS也就是OBJ了 (IE6~8下不兼容)


setTimeout:到达指定时间执行一次函数,执行完成后,当前的定时器就没用了
setInterval:到达指定的时间先把函数执行一次,但是此时定时器并没有失去它的作用,以后每间隔这么长的时间,当前的函数都会重新执行一次,除非手动清除当前的定时器
setTimeout(function () {
    //->this:window
    console.log(this);
}, 1000);
```
**定时器的返回值是一个数字（1+），代表当前定时器是页面中的第几个定时器(可以按照去银行办业务领取的排队号理解)**

>**clearInterval/clearTimeout([NUM])：**
>通过定时器的排队号清除指定的定时器,而且不管是用哪个定时器设置的,任意一个清除方法,只要把排队号指定好,都可以把定时器清除掉,比如：用setInterval设置的定时器，使用clearTimeout也可以把其清除掉(不推荐这样用)
>```
var timer1 = setInterval(function () {
    console.log('ok');
}, 10000);
>
var timer2 = setTimeout(function () {
    console.log('NO');
}, 20000);
clearInterval(2);
>```
####定时器时间设置法则
**定时器的时间因子设置为0,也不是立马执行,**    **`每一个浏览器都有一个最小的反应时间`**
>(预估测试值:谷歌最小的反应时间是5~6ms IE最小反应时间是10~13ms  我们一般设置的时候,最小值设置为17ms性能会更好一些),
>当我们设置的时间小于这个值,浏览器也是按照最小的时间处理的 
> =>也就是设置一个定时器,怎么着也要等一会在执行,此时不等,继续执行下面的任务...
>```javascript
 var n = 12;
 setTimeout(function () {
     n++;
     console.log(n);//->2) 13
 }, 0);
 console.log(n);//->1) 12
>```
###定时器的时间设置
我们给定时器设置一个时间,到达时间定时器一定执行了吗?
**答案：不一定**
>设置一个定时器,总要等一段时间再执行,此阶段我们不等,继续执行下面的任务,但是由于JS的单线程的,一次只能处理一件事情,下面的任务没完成,不管定时器是否到达设定的时间,也要把下面任务彻底完成后,才能反过头执行定时器里面的内容
```javascript
var n = 12;
var sTime = new Date();
setTimeout(function () {
var endTime = new Date();
console.log(endTime - sTime);//-->303
//->测试最小的反应时间
console.log(++n);//-->2) 13
}, 0);

var starTime = new Date();
for (var i = 0; i < 100000000; i++) {

}
var endTime = new Date();
console.log(endTime - starTime); //-->302
//->通过性能测试，我们发现在谷歌下循环一亿次大概需要300MS左右
console.log(n);//-->1) 12
```
**当同步的任务彻底完成后,开始看之前设置的定时器是否到时间,到时间的给予执行**
>如果有很多的定时器都到时间了,会把最先到达时间的先执行(因为在设置定时器的时候,浏览器会把计时最短的定时器排在队列的前面)
>```
->一次都不会输出,因为执行死循环后,当前的浏览器就再也做不了其它的事情了(JS是单线程的)
var n = 12;
setTimeout(function () {
    console.log(++n);
}, 0);
while (1 === 1) {
>
}
console.log(n);
>```
####实战案例
```javascript
需求：开始进来输出1，以后每隔1S钟都累加1，到5结束
var n = 0;
function fn() {
     n++;
     console.log(n);
     if (n >= 5) {
         clearInterval(timer);
     }
}
fn();
var timer = setInterval(fn, 1000);
```
----
**使用递归实现当前的需求:setTimeout模拟出setInterval的效果**
递归：函数执行的时候,在调用自己执行
```
var n = 0,
    timer = null;
function fn() {
    //->执行FN的时候,上一次创建的那个定时器已经没用了,为了节约内存和性能,我们最好把没用的这个定时器给清除掉
    clearTimeout(timer);//->清除上一次设置的定时器

    console.log(++n);
    if (n >= 5) {
        return;
    }
    //->arguments.callee:当前函数本身(JS严格模式下不允许使用,所以真正项目中我们基本上不用这个属性)
    timer = setTimeout(fn, 1000);
}
fn();
```
**需求：让小球从当前位置运动到右边边界的位置(修改小球的LEFT值即可)**
**[步长固定，时间不固定]---------------------**
>```
var box = document.getElementById('box'),
    maxLeft = utils.win('clientWidth') - box.offsetWidth,//->计算出运动目标位置的LEFT值
    step = 20,//->步长:每一次走多少距离
    interval = 17;//->时间因子:多长时间执行一次运动(频率)
>
>
var timer = setInterval(function () {
    var curL = utils.css(box, 'left');
    curL += step;
    utils.css(box, 'left', curL);
    if (curL >= maxLeft) {
        clearInterval(timer);
    }
}, interval);
>```
**优化一：尽量少用全局的变量**
var box = document.getElementById('box'),
    maxLeft = utils.win('clientWidth') - box.offsetWidth;

>真正项目中我们一般很少会把TIMER设置为全局变量(这样会导致变量冲突:可能一个TIMER代表的是另外的定时器了),我们一般都会把它设置在当前需要运动元素的自定义属性上,这样不仅仅防止了冲突,而且在任何时候如果需要,都可以通过自定义属性的方式获取到(不受闭包循环等干扰)
>```
box.timer = setInterval(function () {
    var curL = utils.css(box, 'left');
    curL += 20;
    utils.css(box, 'left', curL);
    if (curL >= maxLeft) {
        clearInterval(box.timer);
    }
}, 17);
>```
>**优化二**
>边界判断:真正项目中我们做边界判断,都是首先拿当前位置加上步长,验证一下累加的值是否那会超过边界,如果已经超过边界了,我们就不要在加步长了,而是让元素直接运动到边界的位置即可...
>```javascript
var box = document.getElementById('box'),
    maxLeft = utils.win('clientWidth') - box.offsetWidth;
box.timer = setInterval(function () {
    var curL = utils.css(box, 'left');
    //->边界判断:如果我在按照现有步长走一步,就已经超过边界了,此时的我们直接让元素运动到边界位置即可(结束动画)
    if (curL + 20 >= maxLeft) {
        utils.css(box, 'left', maxLeft);
        clearInterval(box.timer);
        return;
    }
    utils.css(box, 'left', curL + 20);
}, 17);
>```




---
**[时间固定的匀速动画]-------------**
>**t:time 当前已经走的时间**
**b:begin 起始的位置**
**c:change 总距离**
**d:duration 总时间**

>计算出当前元素的位置




>```javascript
function linear(t, b, c, d) {
    return t / d * c + b;
}
var begin = utils.css(box, 'left'),
    target = utils.win('clientWidth') - box.offsetWidth,
    change = target - begin,
    duration = 500;
var time = 0;
box.timer = setInterval(function () {
    time += 17;
    if (time >= duration) {
    //->已经走的时间大于等于总时间,我们应该结束动画
        utils.css(box, 'left', target);
        clearInterval(box.timer);
        return;
    }
    var curL = linear(time, begin, change, duration);
    utils.css(box, 'left', curL);
}, 17);
>```
**弹出层案例**
```javascript
var dialogBg = document.getElementById('dialogBg'),
    dialog = document.getElementById('dialog'),
    dialogClose = document.getElementById('dialogClose');

document.body.onclick = function () {
    //->让弹出层显示
    utils.css(dialogBg, 'display', 'block');
    utils.css(dialog, 'display', 'block');

    //->让显示内容的提示框区域是从中间放大出来的
    animate(dialog, {
        width: 500,
        height: 400,
        marginLeft: -250,
        marginTop: -200,
        opacity: 1
    }, 200);
};

dialogClose.onclick = function (e) {
    utils.css(dialogBg, 'display', 'none');

    //->首先让弹出层先慢慢的消失
    animate(dialog, {
        width: 0,
        height: 0,
        marginLeft: 0,
        marginTop: 0,
        opacity: 0
    }, 200);
    //->问题：当我们动画结束后，应该让其display=none才可以

    e = e || window.event;
    e.stopPropagation ? e.stopPropagation() : e.cancelBubble = true;//->阻止事件的传播
};
```