# Object Oriented Programing

[TOC]

## 小知识点

- throw "抛出异常"
    `throw new TypeError('"this" is null or not defined');`
- "use strict" 
    - 全部小写,整个字符串是个字符,不能随便添加空格,可以单引号
    - 作用域,在函数内部(顶部), `<script>` 标签内(相互独立)
    
- 反括号  var str =  `字符串` 处理参数过长
- == 判断值 === 判断值和类型  若为引用类型, 则判断 地址

- with
with(对象){对象的作用域,this指向window}省略前缀
添加属性,会添加到window上

## 面向对象 

**私有变量和函数**

    定义在构造函数内部而被this对象的变量,在外部无法访问到的变量和函数

**公有变量和方法**

    对外暴露接口,可以通过构造函数对象创建的对象访问的属性和方法

**代码示例**

```JS
function Car(type,number) {
        this.type = type;   //公共的属性
        this.number = number;
        var city = "广州";                //私有变量
        var getNumber = function () {       //私有函数
            return number;
        };
        var getType = function () {
            return type;
        };

        //能够访问私有变量和函数的方法 --- 特权方法
        this.getDescription = function () {
            console.log(getNumber() + getType() + city);
        }
    }

    var car = new Car("汽车","201718");
    car.getDescription();
```




- prototype (object类型) 是function自带的属性,有一个constructor属性指向该函数,object没有该属性

```
 Object.property中的属性和方法

① constructor 指向原型相关联的构造函数，为Object
② hasOwnProperty 判断对象中是否拥有某个实例属性(不包括原型链上面的属性)
    - hasOwnProperty
    - 对象.hasOwnProperty("属性")
    - 类似in,但是原型对象中的属性不算
③ isPrototypeOf  校验某个对象是否是指定对象的原型对象(整条原型链)
④ propertyIsEnumerable 属性是否存在且可枚举(使用for循环可以遍历,即目标属性能否在for循环中显示出来)
⑤ toString() 返回一个描述目标对象的字符串,对象则返回[object object]
    Object.prototype.toString.call(被检测的参数如 arr) [object Array]
   toString(参数) 参数出可以传入一个用于进制数的参数,该参数的默认值为10(主要针对Number类型有效)
⑥ toLocaleString 同toString,但是会做一些本地化的处理。
⑦ valueOf() 返回指定对象的原始值
             如果该对象有 基本数据类型的值,则返回该值,
             如果没有则返回this本身。
             Date对象调用该方法会返回一个时间戳。
```


### 关键字

- Object.getPrototypeOf(object) 返回obj的原型  ==> 构造函数的原型属性

- break 停止循环 continue 跳过当前 进行下次

- delete 关键字
    - 删除对象的属性
    - 删除没用var 声明的对象
    - delete 属性屏蔽 ->访问原型中的属性.就相当于 实例.prototype.属性
    
- in关键字 
    - 在判断属性是否存在于对象中时,key 是字符串,需要加双引号
    - in 操作array数组时 操作的是索引值 (1 in arrar) 
    - 原型对象上的属性也会被枚举
   
- instanceOf 
  - 对象  instanceOf  构造函数/具体类型   
  - 实例在原型链上就是,对应构造函数的实例 
  
- 对象.constructor
  - (实例的constructor 来自原型对象的constructor 共同指向 构造函数)
  -  constructor 一定指向构造函数



- 修改原型中的属性 
    - 对象.属性 无法操作原型对象中的属性和方法
    - 对象.属性(对象).属性 可以修改原型对象的属性(对象)的属性

- null 变量的值不会为null,除非手动设置

``` JS
# 函数参数是按值传递 
/*如果形参名称 和 全局变量一样时 就近原则 选择num 为形参*/
var num = 10;
function fn(num) {
    num =5;          // 此时修改的为形参, 而全局变量num 没有被修改
    console.log(num); //num = 5
}
fn(num);
console.log(num);  // num =10
```

``` JS
function fn(n) {
    num =5;         // 此时num 为 全局变量 被修改
    console.log(n); //num = 5
}
fn(num);
console.log(num);  // num = 5
```



-------
### 原型链
Fun 和 Obj

![屏幕快照 2017-01-29 上午9.08.22-w600](media/14869708097651/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-01-29%20%E4%B8%8A%E5%8D%889.08.22.png)

![屏幕快照 2017-01-29 上午8.58.36-w600](media/14869708097651/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-01-29%20%E4%B8%8A%E5%8D%888.58.36.png)


### 继承

- 实现 o 继承 tmp 对象 (ECMA5方法)
    - `var o = Object.creat(tmp)` 
    
```JS
var obj = {name ="名称"};
var o = {}
// 单个实例实现继承
o.__proto__ = obj;    
```

```JS
str.name = "名字";     //先创建包装类型,执行完后,对象销毁
console.log(str.name)   // undefined
```

1. 属性 通过call传递  B继承了A的属性

```
 function B{
    A.call(this);
 }
```

2. 遍历传递方法 (若直接赋值传递,是引用了相同的内存对象)

```
for (var i in A.prototype){
    B.prototype[i]=A.prototype[i];
}
```

3. 封闭空间

```
    //1
    (function () {

    })();
    //
    (function () {

    }());

```




- caller 返回函数调用者
    - 场景 主要用于察看函数本身被哪个函数调用

- callee
   - 返回正被执行的 Function 对象，也就是所指定的 Function 对象的正文.
   - callee是arguments 的一个属性成员，它表示对函数对象本身的引用
   - arguments.callee.length可以获取实参参数


- call 
    - 供爷法则:```爷.爷的方法(你,你的参数) ```
    - 作用:将 "爷" 中的this指针 改为 "你"
    - 1 将伪数组
    (document.getbytagname()  arguments $('.class'))
    转换成真数组
    `Array.prototype.slice.call(fackArray);`
    - 2 判断类型:  
      ```tostring.call(123)     [object number]```

- apply
    - 和call一样,参数是数组
    - apply应用 ,保留this指向
  
```js
//因为document.getElementById方法的内部实现中需要使用到this,这个this本来期望指向的是document对象
//当我们以document.getElementById来调用的时候,内部的this指向document对象
//但是当我们以getId的方式调用的时候,内部的this指向的是window对象(因为我们以普通的方式进行调用)

 //借用apply来修正this
document.getElementById = (function (func) {
   return function () {
       return func.apply(document,arguments);
   }
})(document.getElementById);


var getId = document.getElementById;
var div = getId('demo');        //会报错?
console.log(div);
```
    

### 判断类型:
 
 - tostring.call(123)     [object number]
 - []是不是Array的一个实例
 - `[] instanceof Array`
 - `[].constructor === Array `
 - typeof (关键字) 返回值为字符串
    `if(typeof fn == 'Function'){}`

    
    
### 拼接字符串


    
```Js
    // 1 拼接字符串
    var arr1  = [1,2,3];
    var arr2 = [3,4,5];
    arr1.push.apply(arr1,arr2);
    
    // 2 求数组中的最大值
    //(Max只能接受离散值) 这里先转换为 Math.max.call(null,3,4,5);
    Math.max.apply(null,arr2);
```


- format

- 拼接 template 模板 绑定集合

```js
 <!--模板王者演示-->
<script id="arttemplate" type="text/html">
    <h2>{{name}}</h2>
    <ul>
        {{each films}}
            <li>
                <strong>电影名称：</strong>{{$value.title}}<br>
                <strong style='color:red'>导演</strong>{{$value.lead}}
                <strong style='color:green'>主演:</strong>{{$value.role}}
            </li>
        {{/each}}
    </ul>
    </script>
```


###字符串:

```Js
接近数组: concat拼接, indexOf , charAt(index)返回特定位置的字符 
return 'cat'.charAt(1); // returns "a"
return 'cat'[1]; // returns "a"
substr (fromIndex, length)  //删除的长度 
substring(startIndex, endIndex)  //删除截止到
slice(startIndex, endIndex) 
slice可对数组操作，substring不行
    
###字符串 -> 数组 split()分割  *带p的 常用
按给定字符串分割，返回分割后的多个字符串组成的字符串数组。
    
String.prototype.trim()
从字符串的开始和结尾去除空格。参照部分 ECMAScript 5 标准。
```  

### 数组:

```Js
组合记忆 shift unshift pop push
接近符串: 合并concat ,indexOf()返回索引, slice(start, end) 数组截取

//创建一个数组的复制
var shallowCopy = fruits.slice(); 

数组 -> 字符串  join(separator) 数组拼接成字符串

###splice  *带p的 常用 
        splice(start, deleteCount, val1, val2,...) 
        从start位置开始删除,删除deleteCount个,添加val1,val2


// ECMA5  
0.
var fruits =["apple","banana"]
fruits.forEach(function (item, index, array) { //遍历
  console.log(item, index); // Apple 0   Banana 1
});

1.
arr.every(callback[, thisArg]) //不改变原数组,多用来判断
callback  用来测试每个元素的函数。
thisArg   执行 callback 时使用的 this 值。

2.
array.map() 方法返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组。

array.map(callback[, thisArg])

callback 原数组中的元素经过该方法后返回一个新的元素。
currentValue   callback 的第一个参数，数组中当前被传递的元素。
index          callback 的第二个参数，数组中当前被传递的元素的索引。
array          callback 的第三个参数，调用 map 方法的数组。
thisArg        执行 callback 函数时 this 指向的对象。

常用方法:
000. 示例
array.map(function(currentValue, index, array){
    
})

001. 返回数组各值的平方根
var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
/* roots的值为[1, 2, 3], numbers的值仍为[1, 4, 9] */

002. 返回数组对应ASCII
var map = Array.prototype.map
var a = map.call("Hello World", function(x) { 
  return x.charCodeAt(0); 
})

3.
Array.isArray()
假如一个变量是数组则返回true，否则返回false。

4.
Array.prototype.toString()
返回一个由所有数组元素组合而成的字符串。遮蔽了原型链上的 
Object.prototype.toString() 方法。

5. //待定
Array.from() 
从类(伪)数组或者迭代对象（iterable object）中创建一个新的数组实例。

Array.from(arrayLike[, mapFn[, thisArg]])
arrayLike  想要转换成真实数组的类数组对象或可遍历对象。
mapFn   可选参数，如果指定了该参数，则最后生成的数组会经过该函数的加工处理后再返回。
thisArg  可选参数，执行 mapFn 函数时 this 的值。

6. 数组 转 字符串
str = JSON.stringify(array)  
//将JavaScript值转换为JSON字符串
// JSON 序列化
```


###new 的原理
  - 先开辟一个内存空间,先创建一个新的空对象 
  - 把this 指向这个空对象,拷贝函数中的属性和方法
  - 把空对象的 _proto_ 指向 构造函数内部 原型对象 prototype
  - 构造函数执行完成后如果没有 return 把这个新对象返回,(return的是基本数据类型和null,依然返回原对象,因为指针依然指向原对象)

实例拷贝原理: 
实例化的时候,都会将构造函数的属性拷贝一份(包括隐藏属性),同时赋给新值,因为有的构造函数有默认值,就会讲内存空间替换掉

构造函数:
return {}. 代替原对象
return 'jacket' 返回原对象


定义一个构造函数 是不分配内存的
只有实例化的时候 才分配内存






### 引用类型 
 
``` JS
 例题1:
var a = {x:1};
b = a;
a.x = 2;
console.log(b.x);  //2
a = {x:3};
console.log(b.x);  //2

例题2:
 var a = {n:1};
    var b = a;
    a.x = a = {n:2};  
    console.log(a.x);  // undefined
    console.log(b.x);  // {n:2}
    console.log(a);    // {n:2}
    console.log(b)     // {n:1,x:{n:2}
    
 /*
  根据优先级 a.x -> 给原{n:1}对象 添加一个x属性 undefined,
  根据 赋值运算从右往左, 
  a={n:2} -> a 指向一个新对象{n:2},
  a.x = a -> {n:1}.x 指向 {n:2}
  */
```
 

### 深浅拷贝

```Js
function deepCopy(obj1,obj2) {
obj2 = obj2 || {};
for (var i in obj1)
{
  //判断是否是实例属性
  if(obj1.hasOwnProperty(i))
  {
      if (typeof obj1[i] == 'object')
      {
          obj2[i] = Array.isArray(obj1[i])?[]:{};
          // 先创建一个空对象,来接收对象
          deepCopy(obj1[i],obj2[i]); //函数的调用(实参的值赋值给形参)
      }else
      {
          //基础数据类型
          obj2[i] = obj1[i];
      }
  }

}
}
deepCopy(obj,obj2);
```




