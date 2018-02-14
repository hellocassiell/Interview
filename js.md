对javascript核心概念的讲解：对象/原型链/ 构造函数/执行上下文/作用域链/闭包/this




## 原型链
person - proto -> Person.prototype - proto -> Object.prototype - proto -> null

## JavaScript的数据类型都有什么？

基本数据类型：String,Boolean,Number,Undefined, Null

引用数据类型：Object(Array,Date,RegExp,Function)

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
