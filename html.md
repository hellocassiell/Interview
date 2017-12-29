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