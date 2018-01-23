## 常用浏览器及其内核
IE  trident
Firefox  gecko
Safari  webkit
Opera  blink 
Chrome  blink

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
#### 标准模式与怪异模式的常见区别
1. 盒模型的处理差异：
标准CSS盒模型的宽度和高度等于内容区的高度和宽度，不包含内边距和边框，而IE6之前的浏览器实现的盒模型的宽高计算方式是包含内边距和边框的。因此，对于IE，怪异模式和标准模式下的盒模型宽高计算方式是不一样的；
2. 行内元素的垂直对齐：
很多早期的浏览器对齐图片至包含它们的盒子的下边框，虽然CSS的规范要求它们被对齐至盒内文本的基线。标准模式下，基于Gecko的浏览器将会对齐至基线，而在quirks模式下它们会对齐至底部。最直接的例子就是图片的显示。在标准模式下，图片并不是与父元素的下边框对齐的，如果仔细观察，你会发现图片与父元素下边框之间存在一点小空隙。那是因为标准模式下，图片是基线对齐的。而怪异模式下，则不存在这个问题。
<table>元素中的字体：
Quirks Mode 下，对于 table 元素，字体的某些属性将不会从 body 或其他封闭元素继承到 table 中，特别是 font-size 属性。
内联元素的尺寸：
在 Standards Mode 下，non-replaced inline 元素无法自定义大小，而在 Quirks Mode 下，定义这些元素的 width 和 height 属性，能够影响该元素显示的大小尺寸。

3. 元素的百分比高度：
当一个元素使用百分比高度时，在 Standards Mode 下，高度取决于内容的变化，而在 Quirks Mode 下，百分比高度则被正确应用。
元素溢出的处理：
在 Standard Mode 下，overflow 取默认值 visible，即溢出可见，这种情况下，溢出内容不会被裁剪，呈现在元素框外。而在 Quirks Mode 下，该溢出被当做扩展 box 来对待，即元素的大小由其内容决定，溢出不会被裁剪，元素框自动调整，包含溢出内容。

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
## 什么是渐进增强

渐进增强是指在web设计时强调可访问性、语义化HTML标签、外部样式表和脚本。保证所有人都能访问页面的基本内容和功能同时为高级浏览器和高带宽用户提供更好的用户体验。核心原则如下:

- 所有浏览器都必须能访问基本内容
- 所有浏览器都必须能使用基本功能
- 所有内容都包含在语义化标签中
- 通过外部CSS提供增强的布局
- 通过非侵入式、外部javascript提供增强功能
- end-user web browser preferences are respected
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

## div+css的布局较table布局有什么优点？

改版的时候更方便 只要改css文件。
页面加载速度更快、结构化清晰、页面显示简洁。
表现与结构相分离。
易于优化（seo）搜索引擎更友好，排名更容易靠前。

## 强调标签
strong:粗体强调标签，强调，表示内容的重要性
em:斜体强调标签，更强烈强调，表示内容的强调点

## <img>的title和alt有什么区别
1. title是global attributes之一，用于为元素提供附加的advisory information。通常当鼠标滑动到元素上的时候显示。
2. alt是<img>的特有属性，是图片内容的等价描述，用于图片无法加载时显示、读屏器阅读图片。可提图片高可访问性，除了纯装饰图片外都必须设置有意义的值，搜索引擎会重点分析。


## 为什么利用多个域名来存储网站资源会更有效
- CDN缓存更方便 
- 突破浏览器并发限制 
- 节约cookie带宽 
- 节约主域名的连接数，优化页面响应速度 
- 防止不必要的安全问题

## 描述一下cookies，sessionStorage和localStorage的区别　

　 sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

　　web storage和cookie的区别

- Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用。
- 除此之外，Web Storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie。但是Cookie也是不可以或缺的：Cookie的作用是与服务器进行交互，作为HTTP规范的一部分而存在 ，而Web Storage仅仅是为了在本地“存储”数据而生。