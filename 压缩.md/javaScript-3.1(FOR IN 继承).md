##javaScript-3.1(FOR IN 继承)

---
[TOC]

---

####for in循环
>**既可以遍历一个对象私有的属性和方法，也可以遍历到直接所属类的prototype上的属性和方法，但是不能遍历到某些属性（比如：内置属性，还有不可媒举的属性）**
####继承
```
  /*
    function A() {
        this.a="a";
    }
    function B() {
        this.b="b";
        A.call(this);
    }
    var b= new B;
    console.log(b);
    */


    function A() {
        this.a="a";
    }
    A.prototype.getA=function () {};


    function B() {
        this.b="b";
        var objA=new A;
        for(var key in objA){
            //this[key]=objA[key]
            if(objA.hasOwnProperty(key)){
                this[key]=objA[key]
            }else {
                //this.__proto__[key]=objA[key];
                B.prototype[key]=objA[key]
            }
        }
    }
    B.prototype.getB=function () {};
    var b= new B;
    console.log(b);
    //B {b: "b", a: "a"}


    var str="1234";
    var ary=[1,2,3];
    console.log(Object.getOwnPropertyDescriptor(str, "length"));
    //Object {value: 4, writable: false, enumerable: false, configurable: false}
    console.log(Object.getOwnPropertyDescriptor(ary, "length"));
    //Object {value: 3, writable: true, enumerable: false, configurable: false}
```
---
```javascript
B.prototype=Object.assign(B.prototype,A.prototype);
//Object.assign（对象A，对象B），将对象A合并到对象B上，ES6语法，标准浏览器兼容，B没有的数据就给它添加上，B自己有的属性，不会被A的覆盖，
```
---
```
function A() {
        this.a="a";
    }
    A.prototype.getA=function () {};

    function B() {
        this.b="b";
    }
    B.prototype.getB=function () {};
    //B.prototype.__proto__=A.prototype;
    B.prototype=new A;
    var  b=new B;
    b.getA;
    b.__proto__.__proto__.getA
    b.a;
    b.__proto__.a

```