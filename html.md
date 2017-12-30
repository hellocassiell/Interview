## 什么是web语义化,有什么好处
web语义化是指**通过HTML标记表示页面包含的信息**，包含了**HTML标签的语义化**和**css命名的语义化**。 
HTML标签的语义化是指：通过使用包含语义的标签（如h1-h6）恰当地表示文档结构 
css命名的语义化是指：为html标签添加有意义的class，id补充未表达的语义，如Microformat通过添加符合规则的class描述信息 

为什么需要语义化：
- 去掉样式后页面呈现清晰的结构
- 盲人使用读屏器更好地阅读
- 搜索引擎更好地理解页面，有利于收录
- 便团队项目的可持续运作及维护

## 浏览器的标准模式和怪异模式
HTML文档的头部会有文档类型声明：DOCTYPE。当浏览器遇到正确的文档声明时，浏览器就会启动标准模式。
请确定你把 DOCTYPE 正确地放在 HTML 文件的顶端。任何放在 DOCTYPE 前面的东西，比如批注或 XML 声明，会令 Internet Explorer 9 或更早期的浏览器触发怪异模式。
#### 标准模式与怪异模式的两个常见区别
盒模型的处理差异：
标准CSS盒模型的宽度和高度等于内容区的高度和宽度，不包含内边距和边框，而IE6之前的浏览器实现的盒模型的宽高计算方式是包含内边距和边框的。因此，对于IE，怪异模式和标准模式下的盒模型宽高计算方式是不一样的；
行内元素的垂直对齐：
很多早期的浏览器对齐图片至包含它们的盒子的下边框，虽然CSS的规范要求它们被对齐至盒内文本的基线。标准模式下，基于Gecko的浏览器将会对齐至基线，而在quirks模式下它们会对齐至底部。最直接的例子就是图片的显示。在标准模式下，图片并不是与父元素的下边框对齐的，如果仔细观察，你会发现图片与父元素下边框之间存在一点小空隙。那是因为标准模式下，图片是基线对齐的。而怪异模式下，则不存在这个问题。


## XHTML 与 HTML 之间的差异
XHTML 是更严谨更纯净的 HTML 版本。
- XHTML 元素必须被正确地嵌套。
- XHTML 元素必须被关闭。
- 标签名必须用小写字母。
- XHTML 文档必须拥有根元素。

## HTML5 data-* 自定义属性
**进行数据存放**
解决自定义属性混乱无管理的现状

为div添加了一个data-my的自定义属性
```
var test = document.getElementById('test');
        test.dataset.my = 'Byron';
```
使用函数attr()来显示data-parent的内容
```
article::before {
  content: attr(data-parent);
}
```

## [meta标签](https://segmentfault.com/a/1190000004279791)
**元数据**，是用于描述数据的数据。它不会显示在页面上，但是机器却可以识别。

> meta常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。

1. name属性
```
<meta name="参数" content="具体的描述">
```
可选常用参数：
- keywords  用于告诉搜索引擎，你网页的关键字
- description  用于告诉搜索引擎，你网站的主要内容
- viewport  移动端的窗口
-  robots  定义搜索引擎爬虫的索引方式
- author  作者
-  generator 网页制作软件
- copyright  用于标注版权信息
- revisit-after  搜索引擎爬虫重访时间
- renderer  双核浏览器渲染方式

2. http-equiv属性
相当于HTTP的作用，比如说定义一些HTTP参数。
```
<meta http-equiv="参数" content="具体的描述">
```
可选常用参数：
- content-Type(设定网页字符集)(推荐使用HTML5的方式)
```
<meta http-equiv="content-Type" content="text/html;charset=utf-8">  //旧的HTML，不推荐

<meta charset="utf-8"> //HTML5设定网页字符集的方式，推荐使用UTF-8
```
-  X-UA-Compatible(浏览器采取何种版本渲染当前页面)
一般都设置为最新模式:
```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/> //指定IE和Chrome使用最新版本渲染当前页面
```
- [cache-control](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=zh-cn#cache-control)(指定请求和响应遵循的缓存机制)
指导浏览器如何缓存某个响应以及缓存多长时间
```
<meta http-equiv="cache-control" content="no-cache">
```
禁止百度自动转码
```
<meta http-equiv="Cache-Control" content="no-siteapp" />
```
- expires(网页到期时间)
```
<meta http-equiv="expires" content="Sunday 26 October 2016 01:00 GMT" />
```
- refresh(自动刷新并指向某页面)
```
<meta http-equiv="refresh" content="2；URL=http://www.baidu.com/"> //意思是2秒后跳转到百度
```
- Set-Cookie(cookie设定)
如果网页过期。那么这个网页存在本地的cookies也会被自动删除。
```
<meta http-equiv="Set-Cookie" content="name, date"> //格式

<meta http-equiv="Set-Cookie" content="User=Lxxyx; path=/; expires=Sunday, 10-Jan-16 10:00:00 GMT"> //具体范例
```