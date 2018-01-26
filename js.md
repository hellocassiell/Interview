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

 