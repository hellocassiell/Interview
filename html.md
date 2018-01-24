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
  #### 如何判定现在是标准模式还是怪异模式

方法一：执行以下代码
alert(window.top.document.compatMode) ;
//BackCompat  表示怪异模式
//CSS1Compat  表示标准模式

方法二：jquery为我们提供的方法，如下：
alert($.boxModel)
alert($.support.boxModel)

  #### 如何设置为怪异模式

方法一：在页面项部加 <!DOCTYPE HTML PUBLIC “-//W3C//DTD HTML 4.01 Transitional//EN”>
方法二：什么也不加。

  #### 如何设置为标准模式

加入以下任意一种：HTML4提供了三种DOCTYPE可选择：
<!DOCTYPE HTML PUBLIC “-//W3C//DTD HTML 4.01 Transitional//EN” “http://www.w3.org/TR/html4/loose.dtd”>

<!DOCTYPE HTML PUBLIC “-//W3C//DTD HTML 4.01//EN” “http://www.w3.org/TR/html4/strict.dtd”>

<!DOCTYPE HTML PUBLIC “-//W3C//DTD HTML 4.01 Frameset//EN” “http://www.w3.org/TR/html4/frameset.dtd”>

XHTML1.0提供了三种DOCTYPE可选择：

(1)过渡型（Transitional ）
<!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Transitional//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd”>

(2)严格型（Strict ）
<!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Strict//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd”>

(3)框架型（Frameset ）
<!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Frameset//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd”>
  #### 标准模式与怪异模式的常见区别
1. 盒模型的处理差异：
标准CSS盒模型的宽度和高度等于内容区的高度和宽度，不包含内边距和边框，而IE6之前的浏览器实现的盒模型的宽高计算方式是包含内边距和边框的。
2. 行内元素的垂直对齐：
很多早期的浏览器对齐图片至包含它们的盒子的下边框，虽然CSS的规范要求它们被对齐至盒内文本的基线。标准模式下，基于Gecko的浏览器将会对齐至基线，而在quirks模式下它们会对齐至底部。最直接的例子就是图片的显示。在标准模式下，图片并不是与父元素的下边框对齐的，如果仔细观察，你会发现图片与父元素下边框之间存在一点小空隙。那是因为标准模式下，图片是基线对齐的。而怪异模式下，则不存在这个问题。
3. table元素中的字体：
Quirks Mode 下，对于 table 元素，字体的某些属性将不会从 body 或其他封闭元素继承到 table 中，特别是 font-size 属性。

4. 行内元素的高宽：
在Standards模式下，给<span>等行内元素设置wdith和height都不会生效，而在quirks模式下，则会生效。

5. 元素的百分比高度：
当一个元素使用百分比高度时，在 Standards Mode 下，高度取决于内容的变化，而在 Quirks Mode 下，百分比高度则被正确应用。

6. 元素溢出的处理：
在 Standard Mode 下，overflow 取默认值 visible，即溢出可见，这种情况下，溢出内容不会被裁剪，呈现在元素框外。而在 Quirks Mode 下，该溢出被当做扩展 box 来对待，即元素的大小由其内容决定，溢出不会被裁剪，元素框自动调整，包含溢出内容。

7.  使用margin:0 auto在standards模式下可以使元素水平居中，但在quirks模式下却会失效。




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
## 渐进增强与优雅降级
- 渐进增强 
progressive enhancement：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级 
graceful degradation：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。
- 区别：优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要。降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带。　
### 什么是渐进增强

渐进增强是指在web设计时强调可访问性、语义化HTML标签、外部样式表和脚本。保证所有人都能访问页面的基本内容和功能同时为高级浏览器和高带宽用户提供更好的用户体验。核心原则如下:

- 所有浏览器都必须能访问基本内容
- 所有浏览器都必须能使用基本功能
- 所有内容都包含在语义化标签中
- 通过外部CSS提供增强的布局
- 通过非侵入式、外部javascript提供增强功能
- end-user web browser preferences are respected

### 什么是优雅降级

“优雅降级”观点认为应该针对那些最高级、最完善的浏览器来设计网站。而将那些被认为“过时”或有功能缺失的浏览器下的测试工作安排在开发周期的最后阶段，并把测试对象限定为主流浏览器（如 IE、Mozilla 等）的前一个版本。

　　在这种设计范例下，旧版的浏览器被认为仅能提供“简陋却无妨 (poor, but passable)” 的浏览体验。你可以做一些小的调整来适应某个特定的浏览器。但由于它们并非我们所关注的焦点，因此除了修复较大的错误之外，其它的差异将被直接忽略。
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

## 知道的网页制作会用到的图片格式有哪些
png-8，png-24，jpeg，gif，svg。

　　但是上面的那些都不是面试官想要的最后答案。面试官希望听到是Webp,Apng。（是否有关注新技术，新鲜事物）

　　Webp：WebP格式，谷歌（google）开发的一种旨在加快图片加载速度的图片格式。图片压缩体积大约只有JPEG的2/3，并能节省大量的服务器带宽资源和数据空间。Facebook Ebay等知名网站已经开始测试并使用WebP格式。

　　在质量相同的情况下，WebP格式图像的体积要比JPEG格式图像小40%。

　　Apng：全称是“Animated Portable Network Graphics”, 是PNG的位图动画扩展，可以实现png格式的动态图片效果。04年诞生，但一直得不到各大浏览器厂商的支持，直到日前得到 iOS safari 8的支持，有望代替GIF成为下一代动态图标准。

##  PNG,GIF,JPG的区别及如何选
GIF:

8位像素，256色
无损压缩
支持简单动画
支持boolean透明
适合简单动画

JPEG：

颜色限于256
有损压缩
可控制压缩质量
不支持透明
适合照片

PNG：

有PNG8和truecolor PNG
PNG8类似GIF颜色上限为256，文件小，支持alpha透明度，无动画
适合图标、背景、按钮

## 为什么利用多个域名来存储网站资源会更有效
- CDN缓存更方便 
- 突破浏览器并发限制 
- 节约cookie带宽 
- 节约主域名的连接数，优化页面响应速度 
- 防止不必要的安全问题


## 在css/js代码上线之后开发人员经常会优化性能，从用户刷新网页开始，一次js请求一般情况下有哪些地方会有缓存处理？

dns缓存，cdn缓存，浏览器缓存，服务器缓存。

 
## 描述一下cookies，sessionStorage和localStorage的区别　

　 sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

　　web storage和cookie的区别

- Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用。
- 除此之外，Web Storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie。但是Cookie也是不可以或缺的：Cookie的作用是与服务器进行交互，作为HTTP规范的一部分而存在 ，而Web Storage仅仅是为了在本地“存储”数据而生。

## 一个页面上有大量的图片（大型电商网站），加载很慢，你有哪些方法优化这些图片的加载，给用户更好的体验。
- 图片懒加载，在页面上的未可视区域可以添加一个滚动条事件，判断图片位置与浏览器顶端的距离与页面的距离，如果前者小于后者，优先加载。
- 如果为幻灯片、相册等，可以使用图片预加载技术，将当前展示图片的前一张和后一张优先下载。
- 如果图片为css图片，可以使用CSSsprite，SVGsprite，Iconfont、Base64等技术。
- 如果图片过大，可以使用特殊编码的图片，加载时会先加载一张压缩的特别厉害的缩略图，以提高用户体验。
- 如果图片展示区域小于图片的真实大小，则因在服务器端根据业务需要先行进行图片压缩，图片压缩后大小与展示一致。 


## 谈谈以前端角度出发做好SEO需要考虑什么？
- 了解搜索引擎如何抓取网页和如何索引网页

　　你需要知道一些搜索引擎的基本工作原理，各个搜索引擎之间的区别，搜索机器人（SE robot 或叫 web crawler）如何进行工作，搜索引擎如何对搜索结果进行排序等等。

- Meta标签优化

　　主要包括主题(Title)，网站描述(Description)，和关键词（Keywords）。还有一些其它的隐藏文字比如Author（作者），Category（目录），Language（编码语种）等。

- 如何选取关键词并在网页中放置关键词

　　搜索就得用关键词。关键词分析和选择是SEO最重要的工作之一。首先要给网站确定主关键词（一般在5个上下），然后针对这些关键词进行优化，包括关键词密度（Density），相关度（Relavancy），突出性（Prominency）等等。

- 了解主要的搜索引擎

　　虽然搜索引擎有很多，但是对网站流量起决定作用的就那么几个。比如英文的主要有Google，Yahoo，Bing等；中文的有百度，搜狗，有道等。不同的搜索引擎对页面的抓取和索引、排序的规则都不一样。还要了解各搜索门户和搜索引擎之间的关系，比如AOL网页搜索用的是Google的搜索技术，MSN用的是Bing的技术。

- 主要的互联网目录

　　Open Directory自身不是搜索引擎，而是一个大型的网站目录，他和搜索引擎的主要区别是网站内容的收集方式不同。目录是人工编辑的，主要收录网站主页；搜索引擎是自动收集的，除了主页外还抓取大量的内容页面。

- 按点击付费的搜索引擎

　　搜索引擎也需要生存，随着互联网商务的越来越成熟，收费的搜索引擎也开始大行其道。最典型的有Overture和百度，当然也包括Google的广告项目Google Adwords。越来越多的人通过搜索引擎的点击广告来定位商业网站，这里面也大有优化和排名的学问，你得学会用最少的广告投入获得最多的点击。

- 搜索引擎登录

　　网站做完了以后，别躺在那里等着客人从天而降。要让别人找到你，最简单的办法就是将网站提交（submit）到搜索引擎。如果你的是商业网站，主要的搜索引擎和目录都会要求你付费来获得收录（比如Yahoo要299美元），但是好消息是（至少到目前为止）最大的搜索引擎Google目前还是免费，而且它主宰着60％以上的搜索市场。

- 链接交换和链接广泛度（Link Popularity）

　　网页内容都是以超文本（Hypertext）的方式来互相链接的，网站之间也是如此。除了搜索引擎以外，人们也每天通过不同网站之间的链接来Surfing（“冲浪”）。其它网站到你的网站的链接越多，你也就会获得更多的访问量。更重要的是，你的网站的外部链接数越多，会被搜索引擎认为它的重要性越大，从而给你更高的排名。

- 合理的标签使用 