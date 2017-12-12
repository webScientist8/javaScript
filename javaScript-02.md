##javaScript-2
-------------------

[TOC]


-------

###一、函数的核心操作
```
 function sum(num1,num2){
    var total=num1+num2;
    total=total.toFixed(2);
    console.log(total);
 }

 sum(10,20);
```

###二、数据类型转换
####1、把其它数据类型转为数字
  - null和undefined转换为字符串的'null'/'undefined'，但是我们不能操作toString这个方法
```
->[12].toString() =>'12'
    ->[12,13].toString() =>'12,13'
    ->[[[[[1]]]],[[[2]]],[[[[[3]]]]]].toString() =>'1,2,3' (美团面试题)

->({name:'hahah'}).toString() =>'[object Object]' 普通对象调用这个方法不是转换为字符串，而是在检测数据类型(Object.prototype.toString.call())

在什么情况下，我们需要把其它数据类型转换为字符串?
      字符串拼接
        1+'1' =>'11' 加号在JS中不仅仅是数学运算,还有字符串拼接的作用,如果加号的一边遇到了字符串,都是字符串拼接
        1-'1' =>0 除了加号,减法/乘法/除法都是数学运算,会把其它的非数字类型转换为数字类型，在进行运算

1+null+undefined+'12'+[]+undefined+{name:'张三'}+null
        ->1+null <=> 1+0 = 1
        ->1+undefined <=> 1+NaN = NaN
        ->NaN+'12' = 'NaN12'
        ->'NaN12' + [] = 'NaN12'
        ->'NaN12' + undefined = 'NaN12undefined'
        ->'NaN12undefined' + {name:'张三'} = 'NaN12undefined[object Object]'
        ->'NaN12undefined[object Object]'+null = 'NaN12undefined[object Object]null'
```

####2、把其它数据类型转为布尔
```
“0、NaN、null、undefined、空字符串”转换为FALSE，其余的都转换为TRUE

    什么时候需要用到这个转换?
      -> ! / !! / Boolean()
      -> if(12){} 先把12转换为布尔,然后验证真假
    Number('') ->0
    Number('12') ->12
    Number('12.5px') ->NaN
    Number(true) ->1
    Number(false) ->0
    Number(null) ->0
    Number(undefined) ->NaN

    Number({}) ->NaN
    Number([]) ->0
    Number([12]) ->12
    Number([12,23]) ->NaN
    对象转为数字：先把对象转换为字符串(toString)，然后把字符串转换为数字(Number)

  2、把其它数据类型转换为字符串(toString)
    [].toString() ->''
    [12,23].toString() ->'12,23'
    /^\d{11}$/.toString() ->'/^\d{11}$/'
    (function sum(){}).toString() ->"function sum(){}"
    ===
    ({}).toString() ->'[object Object]'

 2.1、把其它数据类型转为布尔
    “0、NaN、null、undefined、空字符串”转换为FALSE，其余的都转换为TRUE

    什么时候需要用到这个转换?
      -> ! / !! / Boolean()
      -> if(12){} 先把12转换为布尔,然后验证真假
```
  ####3、把其它数据类型转换为布尔
    “0、NaN、null、undefined、空字符串” 五个是FALSE，其余都是TRUE
```
    =>情况
     1) ! / !! / Boolean()
     2) if(12){} ->先把12转换为布尔，然后判断条件的真假
什么时候会把对象转化为数字？
      ->Number()
      ->parseInt()
      ->parseFloat()
      ->数学运算
```
  ####4、==在进行比较的时候，如果左右两边的数据类型不一致，我们转换为一致的，在进行比较
```
    对象==对象：比较是的引用地址，地址相同则相等，否则不相等，例如：[]==[] ->false

    对象==数字：对象转换为数字(先转换为字符串,然后再转换为数字)，例如：[]==0 ->true  {}==NaN ->false(NaN和自己以及一切都不相等)

    对象==字符串：把对象和字符串都要转换为数字，然后再进行比较

    对象==布尔：依然是把两边都转换为数字再做比较

    字符串==布尔：都转换为数字

    字符串==数字：字符串转换为数字

    布尔==数字：把布尔转换为数字，例如：true==2 ->false

    null && undefined和其它任何数据类型都不相等，但是两者比较相等，例如：null==undefined ->true  null===undefined ->false  null==0 ->false
```
```
   ![]==false：
     1、![] 把数组转换为布尔(只有五个值为FALSE)然后取反  !true->false
     2、false==false =>true

   []==false：
     1、都转换为数字  []->0  false->0
     2、0==0 =>true


   if('3px'+3){//->'3px3' ->true  (加号在JS除了数学运算还有字符串拼接)
     alert(0);
   }else{
     alert(NaN);
   }
   弹出的结果：'0'

   if('3px'-3){//->NaN
     alert(0);
   }else{
     alert(NaN);
   }
   弹出的结果：'NaN'
```


###三、Math：数学函数，它里面提供了一系列方法，可以让我们操作数字
 - typeof Math =>'object'

 - console.dir(Math) =>在这里可以看到Math中提供的所有方法

  > 1、Math.abs：取绝对值
      Math.abs(-12) =>12
      Math.abs(12)  =>12

  >  2、Math.ceil：向上取整
      Math.ceil(12.2) =>13
      Math.ceil(12.0) =>12
      Math.ceil(-12.2) =>-12

   > 3、Math.floor：向下取整
      Math.floor(12.999) =>12
      Math.floor(-12.999) =>-13

  >  4、Math.round：四舍五入
      Math.round(12.49) =>12
      Math.round(12.5)  =>13 (正数包括五是入)
      Math.round(-12.49) =>-12
      Math.round(-12.5)  =>-12 (负数包括五是舍)
      Math.round(-12.51) =>-13

  >  5、Math.max：获取一堆值中的最大值
      Math.max(12,14,23,13,15)  =>23
      Math.max(12,14,'23','13',15) =>23
      Math.max(12,14,'23','13px',15) =>NaN

  >  6、Math.min：获取一堆值中的最小值

  > 7、Math.PI：圆周率(3.141592653589793)

  >  8、Math.sqrt：开平方
      Math.sqrt(100) ->10

   > 9、Math.pow：某个数的多少次幂(多少次方)
      Math.pow(2,3) ->2的3次方 =>8

   > 10、Math.random：获取[0~1)之间的随机小数
      Math.round(Math.random()*(m-n)+n)：获取[n~m]之间的随机整数
```
      例如：获取12~98之间的随机整数
      for(var i=0;i<100;i++){
         var ran=Math.round(Math.random()*(98-12)+12);
         console.log(ran);
      }

```
###四、string字符串
  - var str='zhufeng';
   - 没一个字符都有自己的“索引”位置，索引从零开始，length的属性存储的是字符串的长度
   - str.length / str['length']
   - str[0]第一个字符   str[str.length-1]最后一个字符

  > 1、charAt / charCodeAt
      charAt：根据索引获取对应位置字符，等价于“str[索引]”，通过中括号方式获取，如果索引不存在，返回的结果是UNDEFINED，charAt做了处理，如果不存在返回的是空字符串
```
      charCodeAt：获取指定索引位置的字符所对应的ASCII码值(UNICODE编码) http://www.asciima.com/

      String.fromCharCode([UNICODE值])：根据ASCII值返回对应的字符
```
  > 2、substr / substring / slice 字符串截取
      substr(n,m)：从索引N开始截取M个字符，如果M不写，就是截取到末尾，N也不写从开头截取，如果M大于最大长度，也是截取到末尾；如果N为负数，M则不起作用，倒着截取N个；
        例如：
          str='zhufeng@qq.com'
          str.substr(-3) =>'com'
```
      substring(n,m)：从索引N开始，找到索引为M处(不包含M)，把找到的截取；M不写也依然是截取到末尾；不支持负数索引；

      slice(n,m)：和SUBSTRING语法一样，但是可以支持负数索引
        例如：
          str='zhufeng@qq.com'
          str.substring(-4,-1) =>''
          str.slice(-4,-1)     =>'.co'  用总长度+负数索引，得到一个正数索引，也就是我们需要的正向索引str.slice((14-4),(14-1)) 总长度14
```
  > 3、toUpperCase / toLowerCase
      toUpperCase：把字符串中的所有字符转化为大写
      toLowerCase：把字符串中的所有字符转化为小写
      
=
  > 4、indexOf / lastIndexOf
      indexOf：获取当前某一个字符，在字符串中第一次出现位置的索引
      lastIndexOf：最后一次出现的索引
```
      如果该字符在字符串中存在，返回的结果是>=0的数字，不存在返回-1，我们根据这个规律可以验证，当前字符串中是否包含某一个字符
      if(str.indexOf('z')>=0){
         //->包含
      }else{
         //->不包含
      }
```
 > 5、split：按照某一个指定的分隔符，把字符串中转换为数组
      var str='2017-07-18';
      str.split('-'); =>["2017", "07", "18"]
      
=
  > 6、replace([old],[new])：实现字符串的替换，在不使用正则的情况下，每一次执行这个方法，只能替换一次
      var str='2017-07-18';
      str=str.replace('-','/'); =>"2017/07-18"
      str=str.replace('-','/'); =>"2017/07/18"

  > 7、match
  > 8、localeCompare
  ...

  console.dir(String.prototype) 可以看到字符串中提供的所有方法


####while循环

  while(条件){
     //->只要条件成立就会一直执行循环体中的内容
  }

  for(var i=0;i<4;i++){
    console.log(i);
  }

  var i=0;
  while(i<4){
     console.log(i);
     i++;
  }

----------------------------------------

####【获取dom元素的8个方法】
document.getElementById("id名")
document.getElementsByClassName('class名')
document.getElementsByTagName('标签名')
document.getElementsByName('name属性')
document.documentElement =>html
document.body=>body
document.querySelector('css选择器') =>获取一个
document.querySelectorAll('css选择器') =>获取多个

####【节点关系属性7个】
childNodes 获取的是所有的子节点
children  获取的是所有的元素子节点 (标签)
parentNode 获取的元素父节点
previousSibling 获取的是上一个哥哥节点
nextSibling 获取的是下一个弟弟节点
firstChild 获取的是第一个子节点
lastChild 获取的是最后一个子节点

####【节点类型4个】
                 nodeType      nodeName      nodeValue
元素节点               1         大写的标签名      null
文本节点               3         #text         文本的内容
注释节点               8         #comment      注释的内容
document              9         #document     null

####【while循环的语法】
while(条件){
    只要条件成立我一直执行循环体中的代码
}

【操作dom元素9个方法】
> 1)document.createElement() 创建一个标签元素
> 2)容器.appendChild(我们要添加的元素)   把我们创建的标签插到指定的容器(末尾)

> 3)oldVal.insertBefore(newVal,oldVal) 把一个元素添加另一个元素的前面

> 4)oldVal.replaceChild(newVal,oldVal) 一个元素把另一个元素替换掉

> 5)元素.cloneNode() 把元素克隆一份 true(深度克隆)  false

> 6)document.body.removeChild(我们要移除的元素)

> 7)setAttribute   设置元素的属性名 (会在html结构中体现出来)

> 8)getAttribute   获取元素的属性名

> 9)removeAttribute 移除元素的属性名


```
    var oDiv = document.createElement('div');
    oDiv.id = 'div1';
    oDiv.style.width = '200px';
    oDiv.style.height = '200px';
    oDiv.style.backgroundColor = 'pink';
    document.body.appendChild(oDiv);

    var oDiv1 = document.createElement('div');
    oDiv1.id = 'div2';
    oDiv1.style.width = '200px';
    oDiv1.style.height = '200px';
    oDiv1.style.backgroundColor = 'red';
    oDiv1.innerHTML = '我是红色的方块';
    //oDiv.parentNode.replaceChild(oDiv1,oDiv);
    oDiv.parentNode.insertBefore(oDiv1, oDiv);

    var clo = oDiv1.cloneNode(true); //把红色的方块克隆了一份
    document.body.appendChild(clo); //把克隆的结果添加到body的末尾
    console.log(clo);

    document.body.removeChild(oDiv);

    var oBox = document.getElementById('box');
    oBox.setAttribute('zhufengIndex', '珠峰培训'); //给元素设置属性名 显示在html的结构中
    var zhufeng = oBox.getAttribute('zhufengIndex') //获取元素的属性名
    console.log(zhufeng); //珠峰培训
    oBox.removeAttribute('zhufengIndex'); //移除元素的属性名

    oBox.className='select'; //class='select'
```


####一、数组
  var ary=[12,'哈哈',true,null,undefined,{},function(){}];

  - 数组中每一项的值可以是任何数据类型的
  - 数组的创建有两种方式：
    > 1、字面量方式
      var ary=[12,23];

   > 2、实例创建方式
      var ary=new Array();
      ->new Array(n)：创建一个长度为N的数组,数组中的每一项是UNDEFINED
      ->new Array(非数字) 或者 new Array(放两项及两项以上)：创建一个数组，并且把括号中的内容当做数组的每一项存储起来

  - 数组率属于对象数据类型的
    typeof [] ->'object'

  - 数组也是由属性名和属性值组成的，每一项的值是它的属性值，它的属性名是数字索引，索引从零开始，LENGTH属性存储的是它的长度

  var ary=[12,23,34]; //->一维数组    ary[1]    ->23
  var ary=[12,[23,34]]; //->二维数组  ary[1][0] ->23
  var ary=[12,[23,[34]]] //->多维数组 ary[1][1][0] ->34

```
var ary = [1, 2, 3, 4];

    //->数组中的每一项求和
    //    var total = null;
    //    for (var i = 0; i < ary.length; i++) {
    //        total += ary[i];
    //    }
    //    console.log(total);

    //ary.join('+') //->"1+2+3+4"
    //eval('1+1') //->2 把字符串变为JS表达式执行

    console.log(eval(ary.join('+')));


```
###二、数组中常用的一些方法
   - console.log(Array.prototype); 数组中提供的所有方法在这都可以看到

   A:方法名及所代表的含义
   B:参数
   C:返回值
   D:操作该方法，原来的数组是否发生了改变

### 1、增、删、改
    ->push：向数组末尾追加新项
      参数:一到多个,需要新增加的内容
      返回值:新增后数组的最新长度
      原有数组是否改变:变
```
      ary[ary.length]=xxx  =>向数组末尾追加一项新的内容,这种方式属于对象键值对的操作

      ary.splice(ary.length,0,'x')

    ->unshift：向数组开头追加新项
      参数:新增加的内容
      返回值:新增后数组的最新长度
      原有数组是否改变:变

      ary.splice(0,0,'x')

    ->shift：删除数组第一项
      参数:无
      返回值:被删除的这一项内容
      原有数组是否改变:变

      ary.splice(0,1)

    ->pop：删除数组最后一项
      参数:无
      返回值:被删除的这一项内容
      原有数组是否改变:变

      ary.length-- =>删除数组最后一项

      ary.splice(ary.length-1)

    ->splice
      splice(n,m)：从索引N开始删除M个元素，返回的结果是一个新的数组，数组中包含被删除的那些内容，原来数组会发生改变
        splice(n) 从索引N开始删除到末尾
        splice(0) 清空数组，原有的内容(被删除的)会以一个新数组返回

      splice(n,m,x)：从索引N开始删除M个元素，把删除的部分用X代替(替换)，返回的结果依然是被删除的内容(放在新数组中的)，原来数组改变
        splice(n,0,x) 把X插入到索引N之前
```

####2、查询
```
    ->slice(n,m)：从索引N开始找到索引M处(不包含M)，把找到的部分以一个新数组返回，原来的数组不变
      slice(n) 从索引N开始找到末尾
      slice(0) 数组的克隆，把原有数组克隆一份一模一样的新数组出来
               <=> slice()
      slice(-4,-1) 和字符串的相同，用总长度加负数索引获取到正数，然后按照正数索引去查找即可 例如：总长度为5 <=> slice(1,4)

      ===

      var ary1=[12,23];
      var ary2=ary1.slice(0); //->克隆的意义在于内容相同，但是隶属于不同的内容空间，属于两个独立的个体
      ary2 ->[12,23]
      ary1==ary2 ->FALSE 是不同的空间地址

    ->concat(数组/数字)：把两个或者多个数组进行拼接，最后合并为一个数组，原来的数组不变

```
####3、转换为字符串
```
    ->toString：把数组转换为字符串，原有数组不变，数组中的每一项在字符串中用逗号隔开

    ->join(字符)：把数组中的每一项按照指定字符拼接成字符串，原有数组不变，和字符串中的SPLIT对应
```
####4、排序和排列的
```
    ->reverse：把数组倒过来排列，原有数组改变

    ->sort：把数组进行排序
      var ary=[1,3,2,4];
      ary.sort() =>[1,2,3,4]
      ary.sort(function(a,b){
         return a-b;//->升序
         return b-a;//->降序
      })

      ary=[12,14,24,4];
      ary.sort() =>[12,14,24,4] 在传递参数的情况下，我们的SORT方法只适用于十位数以下的数字，处理十位数以上的数字，需要传递FUNCTION
```

###后面讲的方法在IE6~8下不兼容
```
    ->indexOf/lastIndexOf：和字符串相同，获取当前项在数组中第一次/最后一次出现位置的索引，如果数组中没有这一项返回的结果是-1(在不考虑兼容的情况下，我们可以根据这个规律验证数组中是否包含某项)

    ->forEach：循环数组中的每一项
    ->map：循环数组中的每一项，相对于FOREACH来说，MAP可以把每一项的值进行修改

    var ary=[12,23,34,45];
    ary.forEach(function(item,index){
        //->item：当前循环这一项的内容
        //->index：当前循环这一项的索引
    });
```
-------------------------------
```
var nowTime = new Date();
    console.log(nowTime.getFullYear());//->年(4位)
    console.log(nowTime.getMonth());//->月(0~11代表1~12月)
    console.log(nowTime.getDate());//->日
    console.log(nowTime.getDay());//->(0~6 日~六)
    console.log(nowTime.getHours());//->小时
    console.log(nowTime.getMinutes());//->分钟
    console.log(nowTime.getSeconds());//->秒
    console.log(nowTime.getMilliseconds());//->毫秒
    console.log(nowTime.getTime());//->获取当前时间距离'1970-01-01 00:00:00'之间的毫秒差

    var str = '2017/7/23 18:00:00';
    console.log(new Date(str));//->把一个时间字符串变为标准的时间对象格式,这样就可以调取上面的方法了 (但是对自付串有格式要求)
    /*
     * 2017-07-23 IE下不兼容
     * 2017/07/23 都可以
     * ...其它格式自己回去百度搜一下
     */

```



















































