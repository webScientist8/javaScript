##javaScript-1
---

[TOC]

---

###一、JS中的数据类型
> 1、基本数据类型(值类型)
	数字(number)
    字符串(string)
    布尔(boolean)：true/false
    null：空(没有)
    undefined：未定义(没有)
 




> 2、引用数据类型
    对象数据类型  object
       {} ->普通对象 object
       [] ->数组         array
       /^$/ ->正则   RegExp
       .....
       function
       Tue Jul 11 2017 17:36:17 GMT+0800 (中国标准时间) ->日期
       
函数数据类型：function

####数字(number)
  0
  1
  1.7
  -1.7
  - NaN：not a number 不是一个有效数字，但是它是number类型的

  - isNaN()：验证一个值是否 不是有效数字，如果结果为true，说明真不是有效数字，反之结果为false代表是一个有效数字  =>如果验证的值非number类型的，浏览器首先会把其它类型的值转换为number的类型的，然后再验证是否为非有效数字
   - Number()：把非数字类型的值转为数字类型(强制转换)
   - parseInt()：把非数字类型的值转为数字类型(非强制转换)

```
 WS：CTRL+SHIFT+/ 添加多行注释
    var a = 12;
     a = '珠峰培训';//->"珠峰培训" 只要用单引号或者双引号包含起来的都是字符串格式的数据
     a = true;//->false
     a = null;
     a = undefined;
     a = {name: '珠峰', age: 8};
     a = [12, 23, 34];
     a = /^(\+|-)?(\d|([1-9]\d+))(\.\d+)?$/;
     a = function () {

     };

    console.log(isNaN(12));
     console.log(isNaN('珠峰'));
     console.log(isNaN('12'));//->false 它是有效数字
     console.log(isNaN('12px'));//->true

    console.log(Number('12')); //->12
    console.log(Number('12px'));//->NaN
    console.log(Number(true));//->1
    console.log(Number(false));//->0
    console.log(Number(null));//->0
    console.log(Number(undefined));//->NaN

    console.log(Number('12px'));//->NaN
    console.log(parseInt('12px'));//->12 从左到右查找，把有效数字字符转换为数字，遇到非有效的数字字符，停止查找
    console.log(parseInt('12px13'));//->12
    console.log(parseInt('12.5px'));//->12  int整数
    console.log(parseFloat('12.5px'));//->12.5 float浮点数(小数) 
    console.log(parseFloat('12.5.8px'));//->12.5

    思考题：parseInt([value],[参数2]) 扩展第二个参数的意思

```
-------------------------------


####一、boolean布尔类型
  > 1、true / false
  > 2、! 先把其它数据类型值转换为布尔类型(只有“0、NaN、null、undefined、空字符串”这五个转换为布尔的FALSE，其余都转换为TRUE)，在把转换的结果取反
  > 3、!! 把其它数据类型转换为布尔类型，等同于(Boolean())

```
console.log(!true);//false
console.log(!'珠峰');//false
```

####二、null和undefined
  1、null：空对象指针(没有)
  2、undefined：未定义(没有)

  郭靖的女朋友是NULL、男朋友是UNDEFINED


####三、对象数据类型object
  var obj={
     name:'王彬翊',
     age:82
  };
  obj是对象名
    name和age：属性名(key键)
    '王彬翊'和82：属性值(value值)

    对象就是由多组键值对组成的，每一组之间用逗号隔开
```
var num = 12;
     var obj = {
     name: '许潇文',
     age: 13
     };

    var num1 = 12;
     var num2 = num1; //->把num1的值赋值给num2
     num2 = 13;
     console.log(num1);

     var obj1 = {age: 18};
     var obj2 = obj1; //->把obj1的值赋值给obj2
     obj2.age = 20;
     console.log(obj1.age);

    //->思考题:
    var obj1 = {num: 12};
    var obj2 = obj1;
    obj2 = {num: 13};
    console.log(obj1.num);
```
```
 var obj = {
     name: '王彬翊',
     age: 82
     };

    obj.age = 28;//->修改:因为AGE已经存在(一个对象中的KEY是不能重复的)
     obj.sex = 'MAN';//->增加:之前没有SEX这个KEY

     console.log(obj.name);//->获取

     obj.age = null;//->假删除:把值赋值为NULL,但是该属性还存在
     delete obj.sex;//->真删除:把KEY和VALUE在对象中都移除了

     console.log(obj.age);//->null
     console.log(obj.sex);//->undefined


    var num = 12;
     console.log(num);//->此处是变量，代表的是自身存储的值 =>12
     console.log('num');//->此处是字符串，代表的就是本身'num' =>'num'
     

    var obj = {
     name: '王彬翊',
     age: 82
     };
     console.log(obj['name']);//->此处的'name'是个字符串，代表的就是本身的意思，这里获取的是OBJ中属性名为NAME的属性值 =>'王彬翊'  等价于 obj.name

     //obj[xxx] ->获取属性名为xxx的属性值

     var num = 'age';
     console.log(num);//->'age'
     console.log(obj[num]);//-> obj['age'] 获取AGE的属性值
     console.log(obj['num']);//-> obj['num'] 获取NUM属性名对应的属性值*/

    var ary = [12, 23, 34];
    console.dir(ary);
    //->数组也是对象，数组的属性名是数字，我们看到的是属性值
    /*{
        0:12,  ->0是它第一项的属性名也是它的索引
        1:23,
        2:34,
        length:3  ->数组天生就有的属性，代表数组的长度
    }
    ary['0'] <=> ary[0]
    ary.0 //->如果属性名是数字，只能用中括号的方式，点的方式不支持
    ary.length  <==> ary['length']*/
```

####四、JS中的判断语句
 > 1、if、else if、else
   if(条件1){
      //->如果条件1成立,执行这里的代码,如果不成立往下走
   }else if(条件2){
      //->条件1不成立，条件2成立，执行这里面的代码
   }else if(条件3){
      //->条件1/2都不成立，条件3成立，执行这里面的代码
   }
   ...
   else{
      //->以上条件都不成立，执行这里面的代码
   }

```
 /*num++ <=> num+=1 <=> num=num+1;
      num--;
      num+=2 <=> num=num+2;*/

   var num = 12;
       if (num >= 10) {
           num++;
       } else if (num < 10 && num >= 0) {//-> ||只有一个成立就成立  &&都成立才成立
           num--;
       } else {
           num += 2;
        }
        console.log(num);

  if (1) {//->条件是单独的一个值，首先把这个值转换为布尔，验证真假即可
            console.log('ok');//OK
        }

  if (12 == '12') {
            console.log('ok');//OK
        }
    /*
     * JS中等于号的三种情况：
     *  =：赋值
     *  ==：比较(不限制类型,如果左右两边比较的数据类型不一样,先会转成一样的,然后再进行比较)
     *    12 == '12' =>首先把'12'变为数字12 =>true
     *  ===：绝对比较(必须保证左右两边的数据类型一致才会进行下一步的比较，如果不一致直接是FALSE)
     *    12==='12' =>false
     */

    //->BAT面试题
    var num = Number('12px'); //->NaN
    if (num == 12) {
        console.log(12);
    } else if (num === '12') {
        console.log('12');
    } else if (num === NaN) {//->NaN===NaN：false 不是一个数的范围很广，是没有办法进行比较的，NaN和任何值都不相等
        console.log(NaN);
    } else {
        console.log('啥也不是');//啥也不是
    }
```


> 2、三元运算符
   条件?条件成立做的事:条件不成立做的事;
```
   var num=12;
   if(num>10 && num<20){
      num++; //-> num+=1 -> num=num+1 自身基础上加1
   }else{
      num--;
   }
   console.log(num); =>13

   num>10 && num<20?num++:num--;

```
  > 3、switch case
```
   var num=10;
   switch(num){
      case 1://->CASE后面放入的都是一个具体的值，验证NUM的值是否和这个值相等，如果相等，条件成立，否则不成立
        num++;
        break;//->每一种CASE情况结束，我们需要加一个BREAK，终止判断，下面的验证不在执行
      case 5:
        num+=2;
        break;
      case 10://->每一种CASE情况验证是否相等，都是使用===来验证的，所以保证数据类型也要一致才可以
        num--;
        break;
      default://->以上每一种情况都不成立，执行DEFAULT下面的代码
        num-=2;
   }

    
```
```
 var num = 12;
    if (num > 0) {
        num++;
    } else {
        num--;
    }
    num > 0 ? num++ : num--;

    num > 0 ? (num < 10 ? num++ : num--) : (num > -5 ? num += 2 : num -= 3);
    if (num > 0) {
        if (num < 10) {

        } else {

        }
    } else {
        if (num > -5) {

        } else {

        }
    }

```

###二、循环->FOR循环
 FOR IN循环(回去后看第一周视频:第13个)

```
 for(设置初始值;设置循环成立的条件;步长操作){
    //->循环体
 }

 例如：
 for(var i=0;i<5;i++){
    //->循环体:需要重复做的事情
    console.log(i);//->0 1 2 3 4
 }
 console.log(i);//->5



 for(var i=5;i>1;i-=2){
    console.log(i);//->5 3
 }
 console.log(i);//->1

----------------------------

 for(var i=0;i<10;i++){
    if(i<5){
      i+=2;
    }else{
      i+=3;
    }
    console.log(i);
 }
 console.log(i);

 2 5 9 10
 
----------------------------------
循环体中出现的关键词：
 break：结束整个循环
 continue：结束本轮循环，下一轮还会继续

  for(var i=0;i<10;i++){
     if(i<5){
       i+=2;
       continue;
     }else{
       i+=3;
       break;
     }
     console.log(i);
  }
  console.log(i);//->9


```

 /*itar [TAB]*/
```
     * 循环的四步曲
     * 1、设置初始值
     * 2、验证是否循环的条件
     * 3、条件成立执行循环体中内容，不成立结束循环
     * 4、执行步长累加的操作
```

```
for (var i = 10; i > 0; i -= 2) {
     console.log(i);//->10 8 6 4 2
     }
    for (var i = 10; i > 0; i -= 2) {

     }
     console.log(i);//->0

    /* i*=2 ->i=i*2 ->i=i/2 ->i=i%2 */

        for (var i = 0; i < 9; i += 3) {
            if (i < 5) {
                i += 2;
            } else {
                i--;
            }
            console.log(i);//0 2 4 6
        }
       console.log(i);// 9


        for (var i = 0; i < 5; i++) {
            i < 5 ? i++ : null;//->条件不成立我们什么都不做(不写NULL不符合三元运算符的语法)
            break;
            console.log(i);//->永远不会执行的
        }
        console.log(i);//->执行   //1

    for (var i = 0; i < 9; i += 3) {
        if (i < 5) {
            i += 2;
            continue;
        } else {
            i--;
            break;
        }
        console.log(i);
    }
    console.log(i);//4
```


####for in循环
   用来遍历一个对象中所有键值对的
   for(var key in obj){
      //->obj中有多少组键值对，我们就循环多少次
      key =>键
      obj[key] =>值
   }


###三、函数数据类型
```
  function [函数名](){
     //->函数体：我们把实现当前功能或者需要做事情的那些代码，全部的放在函数体中
  }

  例如：
  function sum(){

  }

  sum(); //->把上面的方法执行，而且可以执行很多次
  sum();
  sum();
  ...
```
  - 函数其实就是一个方法或者一个功能，使用它能够做某些事情，例如：我们可以把家里面的洗衣机理解为一个函数，使用它可以洗衣服

  - 函数有两部分：创建一个函数(购买了一台洗衣机)、执行函数(使用洗衣机洗衣服)，只创建了但是没有执行，函数没有任何的意义

```

//    =>减、乘、除都是数学运算，遇到非数字类型，先转换为数字，然后再进行运算
        console.log('1' - 1);//->0
        console.log(null - 1);//->-1
        console.log(undefined - 1);//->NaN

    //=>加法不仅仅是数学运算，还有字符串拼接的效果
        console.log(1 + null);//->1
        console.log(1 + undefined);//->NaN
        console.log(1 + '1');//->'11' 在JS中遇到了加号，如果有一头是字符串，则代表的不是数字相加，而是字符串拼接

    console.log(1 + null + '10' + undefined + null);
    //1+null ->1
    //1+'10' ->'110'
    //'110'+undefined ->'110undefined'
    //'110undefined'+null ->'110undefinednull'
```
- 数据类型检测
```
//=>JS中数据类型检测的四种方式
  -> typeof：用来检测数据类型的逻辑运算符
  -> instanceof：检测某一个实例是否属于这个类
  -> constructor：通过构造函数检测
  -> Object.prototype.toString.call()：最常用的，借用Object基类原型上的toString方法，在执行这个方法的时候，让方法中的THIS指向需要检测的值，从获取到当前值所属的类，从而检测出对应的数据类型

    //->typeof [value] 检测当前值的数据类型，返回的结果：首先是一个字符串，其次字符串中包含了对应的数据类型
    console.log(typeof 12);//->'number'
     console.log(typeof true);//->'boolean'
     console.log(typeof '12');//->'string'
     console.log(typeof null);//->'object' NULL是空对象指针，率属于基本数据类型，但是使用TYPEOF检测出的结果是'OBJECT' =>这是TYPEOF的局限，我们无法使用这种方式检测NULL
     console.log(typeof undefined);//->'undefined'
     console.log(typeof {});//->'object'  TYPEOF检测数组、正则等结果都是'OBJECT'，也就是我们无法使用这种方式细分对象中的数据类型
     console.log(typeof []);//->'object'
     console.log(typeof /^$/);//->'object'
     console.log(typeof function () {});//->'function'

    console.log(typeof typeof typeof []);
    //-> typeof [] =>'object'
    //-> typeof 'object' =>'string'
    //-> typeof 'string' =>'string'

BAT面试题：
     console.log(typeof typeof []);
       -> typeof [] =>"object"
       -> typeof "object" =>"string"
```
- 函数
```
/*
     * 计算168.3642和247.5621两个数字的和，把获取的和保留小数点后面两位，然后再控制台输出
     */
    //    var total = 168.3642 + 247.5621;
    //    total = total.toFixed(2);//->toFixed:保留小数点后面两位,得到的结果是字符串格式的
    //    console.log(total);

    function sum() {
        var total = 168.3642 + 247.5621;
        total = total.toFixed(2);
        console.log(total);
    }
    sum();
    sum();
    sum();
    sum();

    //->低耦合、高内聚：减少页面中的冗余代码，提高代码的重复利用率 =>函数的作用：把实现一个功能的代码进行封装(封装成一个函数)，以后再想实现这个功能，只需要执行函数即可，无需重复编写代码 =>封装
```

- 函数-形参
```
//->形参：形式参数，给当前函数提供入口，函数执行的时候，我们可以通过入口给函数体中传递一些内容(当我们需要完成一件事，但是原材料不知道，执行的时候，用户传递的时候才知道，此时我们就可以定义形参来解决)
    function sum(num1, num2) {//->num1和num2就是形参(变量)
        var total = num1 + num2;
        total = total.toFixed(2);
        console.log(total);
    }
    sum(100, 200);//->实参：执行的时候给函数形参变量传递的那个值叫做实参(值) num1=100 num2=200
    sum(100);//->num1=100 num2=undefined 定义了形参,执行的时候不传递值，默认形参的值是undefined
```



####string字符串
  -> 所有用''或者""包含起来的都是字符串
  -> [string].length：获取当前字符串中有多少个字符
  -> 字符串中的每一个字符都有自己的位置，而且对应一个数字 =>"索引":索引从0开始，0->第一个字符  2->第三个字符  str.length-1->最后一个字符
  -> str[0] ->获取第一个字符
  -> str[1] ->获取第二个字符
  -> str[str.length-1] ->获取最后一个字符
  str[索引] ->获取指定索引位置的字符





####[]数组
  var ary = [12,'JS',false,null,undefined];

    0:12
    1:'JS'
    ..
    4:undefined
    length:5

  数组的属性名是代表某一项位置的“索引”(索引是从零开始的)，索引0->第一项...
  数组中有一个LENGTH属性代表数组的长度：ary.length / ary['length']

    ary.1  (NO)
    ary[1] (OK)

=========================

###8、基本数据类型和引用数据类型的区别?

  var num1=12;
  var num2=num1; //->把NUM1存储的值赋值给NUM2
  num2=13;
  console.log(num1);

  var obj1={n:100};
  var obj2=obj1;
  obj2.n=200;
  console.log(obj1.n);


  //->思考题：
  var think1={n:100};
  var think2=think1;
  think2={n:200};
  console.log(think1.n);
