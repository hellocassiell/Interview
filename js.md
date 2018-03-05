对javascript核心概念的讲解：对象/原型链/ 构造函数/执行上下文/作用域链/闭包/this




## 原型链
person - proto -> Person.prototype - proto -> Object.prototype - proto -> null

## javascript做类型判断的方法有哪些？
共定义了 7 种数据类型，分为 基本类型 和 引用类型 两大类：
基本类型：String、Number、Boolean、Symbol、Undefined、Null 
占据空间固定，是简单的数据段，为了便于提升变量查询速度，将其存储在栈中，即按值访问
引用类型：Object
其值存储在堆(heap)中，而存储在变量处的值，是一个指针，指向存储对象的内存处，即按址访问
1. typeof
```
typeof ''; // string 有效
typeof 1; // number 有效
typeof Symbol(); // symbol 有效
typeof true; //boolean 有效
typeof undefined; //undefined 有效
typeof null; //object 无效
typeof [] ; //object 无效
typeof new Function(); // function 有效
typeof new Date(); //object 无效
typeof new RegExp(); //object 无效
```
- 对于基本类型，除 null 以外，均可以返回正确的结果。对于 null ，返回 object 类型。
- 对于引用类型，除 function 以外，一律返回 object 类型。
- 在实际的项目应用中，typeof只有两个用途，就是检测一个元素是否为undefined，或者是否为function。
> null 有属于自己的数据类型 Null ， 引用类型中的 数组、日期、正则 也都有属于自己的具体类型，而 typeof 对于这些类型的处理，只返回了处于其原型链最顶端的 Object 类型，没有错，但不是我们想要的结果。
2. instanceof 

A instanceof B，如果 A 是 B 的实例，则返回 true,否则返回 false。
**instanceof 检测的是原型**
instanceof 只能用来判断两个对象是否属于实例关系， 而不能判断一个对象实例**具体**属于哪种类型。
例：instanceof 能够判断出 [ ] 是Array的实例，且它认为 [ ] 也是Object的实例，因为存在一条这样的原型链

> instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。
```
var iframe = document.createElement('iframe');
document.body.appendChild(iframe);
xArray = window.frames[0].Array;
var arr = new xArray(1,2,3); // [1,2,3]
arr instanceof Array; // false
```
针对数组的这个问题，ES5 提供了 Array.isArray() 方法 。该方法用以确认某个对象本身是否为 Array 类型，而不区分该对象在哪个环境中创建。
Array.isArray() 本质上检测的是对象的 [[Class]] 值，[[Class]] 是对象的一个内部属性，里面包含了对象的类型信息，其格式为 [object Xxx] ，Xxx 就是对应的具体类型 。对于数组而言，[[Class]] 的值就是 [object Array] 。

3. Object.prototype.toString()

toString() 是 Object 的原型方法，调用该方法，默认返回当前对象的 [[Class]] 。这是一个内部属性，其格式为 [object Xxx] ，其中 Xxx 就是对象的类型。

对于 Object 对象，直接调用 toString()  就能返回 [object Object] 。而对于其他对象，则需要通过 call / apply 来调用才能返回正确的类型信息。
```
Object.prototype.toString.call('') ;   // [object String]
Object.prototype.toString.call(1) ;    // [object Number]
Object.prototype.toString.call(true) ; // [object Boolean]
Object.prototype.toString.call(Symbol()); //[object Symbol]
Object.prototype.toString.call(undefined) ; // [object Undefined]
Object.prototype.toString.call(null) ; // [object Null]
Object.prototype.toString.call(new Function()) ; // [object Function]
Object.prototype.toString.call(new Date()) ; // [object Date]
Object.prototype.toString.call([]) ; // [object Array]
Object.prototype.toString.call(new RegExp()) ; // [object RegExp]
Object.prototype.toString.call(new Error()) ; // [object Error]
Object.prototype.toString.call(document) ; // [object HTMLDocument]
Object.prototype.toString.call(window) ; //[object global] window是全局对象 global 的引用
```


## 如何判断某变量是否为数组数据类型
- 方法一.判断其是否具有“数组性质”，如slice()方法。可自己给该变量定义slice方法，故有时会失效
- 方法二.obj instanceof Array 在某些IE版本中不正确
- 方法三.方法一二皆有漏洞，在ECMA Script5中定义了新方法Array.isArray(), 保证其兼容性，最好的方法如下：
```
if(typeof Array.isArray==="undefined")
{
  Array.isArray = function(arg){
        return Object.prototype.toString.call(arg)==="[object Array]"
    }; 
}

```

## 什么是Ajax和JSON，它们的优缺点

Ajax是异步JavaScript和XML，用于在Web页面中实现异步数据交互。

优点：

可以使得页面不重载全部内容的情况下加载局部内容，降低数据传输量
避免用户不断刷新或者跳转页面，提高用户体验
缺点：

对搜索引擎不友好
要实现ajax下的前后退功能成本较大
可能造成请求数的增加
跨域问题限制
JSON是一种轻量级的数据交换格式，ECMA的一个子集

优点：轻量级、易于人的阅读和编写，便于机器（JavaScript）解析，支持复合数据类型（数组、对象、字符串、数字）


## 原生JS操作DOM的方法有哪些？
获取节点的方法getElementById、getElementsByClassName、getElementsByTagName、 getElementsByName、querySelector、querySelectorAll,对元素属性进行操作的 getAttribute、 setAttribute、removeAttribute方法，对节点进行增删改的appendChild、insertBefore、replaceChild、removeChild、 createElement等
## 下面这个ul，如何点击每一列的时候alert其index?（闭包）
```
<ul id=”test”>
    <li>这是第一条</li>
    <li>这是第二条</li>
    <li>这是第三条</li>
</ul>
```

```
// 方法一：
var lis=document.getElementById('2223').getElementsByTagName('li');
for(var i=0;i<3;i++)
{
    lis[i].index=i;
    lis[i].onclick=function(){
        alert(this.index);
    };
}
 
//方法二：
var lis=document.getElementById('2223').getElementsByTagName('li');
for(var i=0;i<3;i++)
{
    lis[i].index=i;
    lis[i].onclick=(function(a){
        return function() {
            alert(a);
        }
    })(i);
}
```
## JS常见的dom操作api

## 解释一下事件冒泡和事件捕获
事件冒泡

微软提出 事件从最内层的元素开始发生，一直向上传播

事件捕获

网景提出 事件从最外层开始发生，直到最具体的元素

统一标准

先捕获再冒泡
addEventListener(event, function, useCapture)
useCapture默认值为false 在事件冒泡阶段处理函数
若为true 则在事件捕获阶段处理函数

## typeof操作符返回值有哪些，对undefined、null、NaN使用这个操作符分别返回什么
typeof的返回值有undefined、boolean、string、number、object、function、symbol。对undefined 使用返回undefined、null使用返回object，NaN使用返回number


## 事件委托（手写例子），事件冒泡和捕获，如何阻止冒泡？如何组织默认事件？
## 对闭包的理解？什么时候构成闭包？闭包的实现方法？闭包的优缺点？
## this有哪些使用场景？跟C,Java中的this有什么区别？如何改变this的值？
1. 作为对象的方法调用
this指向该对象
```
var obj = {
  a: 1,
  getA: function() {
    console.log(this === obj);
    console.log(this.a);
  }
};
obj.getA(); // true , 1
```
2. 作为普通函数调用
this总是指向全局对象(浏览器中是window)
```
/**
 * 2.作为普通函数调用
 *
 * 不作为对象属性调用时,this必须指向一个对象。那就是全局对象。
 */
window.name = 'globalName';
var getName = function() {
  console.log(this.name);
};
getName(); // 'globalName'
var myObject = {
  name: "ObjectName",
  getName: function() {
    console.log(this.name)
  }
};
myObject.getName(); // 'ObjectName'
// 这里实质上是把function() {console.log(this.name)}
// 这句话赋值给了theName。thisName在全局对象中调用，自然读取的是全局对象的name值
var theName = myObject.getName;
theName(); // 'globalName'
```

3. 构造器调用
this指向返回的这个对象
```
var myClass = function() {
  this.name = "ll";
};
var obj = new myClass();
console.log(obj.name); // ll
console.log(obj) // myClass {name: "ll"}

```
但是如果构造函数中手动指定了return其它对象，那么this将不起作用。
如果return的是别的数据类型，则没有问题。
```
var myClass = function() {
  this.name = "ll";
  // 加入return时，则返回的是别的对象。this不起作用。
  return {
    name:"ReturnOthers"
  }
};
var obj = new myClass();
console.log(obj.name); // ReturnOthers
```
4. apply和call调用
## call，apply，bind
## 显示原型和隐式原型，手绘原型链，原型链是什么？为什么要有原型链
## 创建对象的多种方式
## 实现继承的多种方式和优缺点
## new 一个对象具体做了什么

1.构造一个新的对象

2.将构造函数的作用域赋给新对象（也就是说this指向了新的对象）

3.执行构造函数中的代码

4.返回新对象
## 手写Ajax，XMLHttpRequest
通过实例化一个XMLHttpRequest对象得到一个实例，调用实例的open方法为这次 ajax请求设定相应的http方法、相应的地址和以及是否异步，当然大多数情况下我们都是选异步， 以异步为例，之后调用send方法ajax请求，这个方法可以设定需要发送的报文主体，然后通过 监听readystatechange事件，通过这个实例的readyState属性来判断这个ajax请求的状态，其中分为0,1,2,3,4这四种 状态，当状态为4的时候也就是接收数据完成的时候，这时候可以通过实例的status属性判断这个请求是否成功
```
var xhr = new XMLHttpRequest();
xhr.open('get', 'aabb.php', true);
xhr.send(null);
xhr.onreadystatechange = function() {
  if(xhr.readyState==4) {
    if(xhr.status==200) {
      console.log(xhr.responseText);
    }
  }
}
```
## 变量提升


## 原生js字符串方法有哪些？
简单分为获取类方法，获取类方法有charAt方法用来获取指定位置的字符，获取指定位置字符的unicode编码的charCodeAt方法， 与之相反的fromCharCode方法，通过传入的unicode返回字符串。查找类方法有indexof()、lastIndexOf()、search()、match() 方法。截取类的方法有substring、slice、substr三个方法，其他的还有replace、split、toLowerCase、toUpperCase方法。