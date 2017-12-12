##javaScript-4.1(重构函数)
---
[TOC]

---
####JS高阶编程技巧：惰性思想


>第一次加载页面,在给utils赋值的时候,执行一个自执行函数,形成一个不销毁的私有作用域,在这个作用域中定义一个变量来存储当前的浏览器是否兼容某个属性或者方法

>以后在getCss等其他的方法中,如果再需要判断是否兼容,就没必要在检测一次了,直接使用这个变量的值即可

>能够执行一次就解决的,绝对不执行多次,这种`懒思想`就是惰性思想,基于这个思想构造的单例模式是“高级单例模式”
>第一次执行函数,我们判读兼容哪一个,然后把方法进行重新赋值,让其只等于兼容的哪一个即可,第二次及


```
var utils = (function () {
    var isCompatible = 'getComputedStyle' in window;

    function getCss(curEle, attr) {
        if (isCompatible) {
            return window.getComputedStyle(curEle, null)[attr];
        } else {
            return curEle.currentStyle[attr];
        }
    }

    return {
        getCss: getCss
    }
})();
```
####JS惰性思想:重构函数
>>**第一次执行函数,我们判断兼容哪一个,然后把方法进行重新赋值,让其只等于兼容的哪一个即可,第二次及以后再执行的时候,直接的运行重构后的方法,告别了复杂的判断**
```
function getCss(curEle, attr) {
    if ('getComputedStyle' in window) {
        getCss = function (curEle, attr) {
            return window.getComputedStyle(curEle, null)[attr];
        };
    } else {
        getCss = function (curEle, attr) {
            return curEle.currentStyle[attr];
        };
    }
    return getCss(curEle, attr);
}
```

**思考题:**
>时间字符串格式化
var str = '2017-8-9 16:43:5';
把这个字符串可以变为 'xxxx年xx月xx日 xx时xx分xx秒' / 'xx-xx xx:xx 08-09 16:43' ... 变为一切你想需要的格式


```
String.prototype.myFormatTime = function myFormatTime(template) {
//     //->this:str 我们需要格式化时间的字符串
//     var ary = this.match(/\d+/g),
//         result = template || '{0}年{1}月{2}日 {3}时{4}分{5}秒';
//     result = result.replace(/\{(\d+)\}/g, function () {
//         var index = arguments[1],
//             value = ary[index] || '0';
//         return value.length < 2 ? '0' + value : value;
//     });
//     return result;
// };
// var str = '2017-8-9';
// console.log(str.myFormatTime());
// console.log(str.myFormatTime('{1}-{2} {3}:{4}'));
// console.log(str.myFormatTime('{0}年{1}月{2}日'));
```


2、URL参数格式化
var url = 'http://www.zhufengpeixun.com/index.html?name=zxt&age=28&sex=1&type=0';
问号以后的都是`URL问号传参值`，接下里我们要把问号后面的信息拆解成为对象的键值对
{name:'zxt',age:28,sex:1,type:0}


```javascript
正则处理
var obj = {};
var reg = /([^?&=]+)=([^?&=]+)/g;//->当前正则匹配的是 xxx=xxx
url.replace(reg, function () {
arguments[1] -> key  第一个分组内容
arguments[2] -> value 第二个分组内容
obj[arguments[1]] = arguments[2];
});
console.log(obj);
```


**把URL问号传递的参数值格式化为一个JSON对象**


```
String.prototype.myQueryURLParameter = function myQueryURLParameter() {
    //->this:url 我们需要处理的URL地址
    var obj = {},
        reg = /([^?&=]+)=([^?&=]+)/g;
    this.replace(reg, function () {
        obj[arguments[1]] = arguments[2];
    });
    return obj;
};
console.log(url.myQueryURLParameter());
```