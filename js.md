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
## 事件委托（手写例子），事件冒泡和捕获，如何阻止冒泡？如何组织默认事件？
## 对闭包的理解？什么时候构成闭包？闭包的实现方法？闭包的优缺点？
## this有哪些使用场景？跟C,Java中的this有什么区别？如何改变this的值？
## call，apply，bind
## 显示原型和隐式原型，手绘原型链，原型链是什么？为什么要有原型链
## 创建对象的多种方式
## 实现继承的多种方式和优缺点
## new 一个对象具体做了什么
## 手写Ajax，XMLHttpRequest
## 变量提升
