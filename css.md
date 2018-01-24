## 有哪些方式可以对一个DOM设置它的CSS样式

- 外部样式表，引入一个外部css文件
- 内部样式表，将css代码放在 <head> 标签内部
- 内联样式，将css样式直接定义在 HTML 元素内部

## css性能优化
- 嵌套层级不要超过3级

## 盒模型
在标准模式下，一个块的总宽度=width+margin(左右)+padding(左右)+border(左右)
在怪异模式下，一个块的总宽度=width+margin（左右）（既width已经包含了padding和border值）
#### box-sizing
```
box-sizing:content-box || border-box || inherit;
```
当设置为box-sizing:border-box时，将采用怪异模式解析计算

## CSS选择器
- *通用选择器：选择所有元素，不参与计算优先级，兼容性IE6+
- 派生选择器（用HTML标签申明）
- id选择器（用DOM的ID申明）
- 类选择器（用一个样式类名申明）
- 属性选择器（用DOM的属性申明，属于CSS2，IE6不支持，不常用，不知道就算了）
　　除了前3种基本选择器，还有一些扩展选择器，包括

- 后代选择器（利用空格间隔，比如div .a{  }）
- 群组选择器（利用逗号间隔，比如p,div,#a{  }）
- :link，：visited，：focus，：hover，：active链接状态： 选择特定状态的链接元素，顺序LoVe HAte，兼容性: IE4+
- X + Y 直接兄弟选择器：在X之后第一个兄弟节点中选择满足Y选择器的元素，兼容性： IE7+
- X > Y 子选择器： 选择X的子元素中满足Y选择器的元素，兼容性： IE7+
- X ~ Y 兄弟选择器： 选择X之后所有兄弟节点中满足Y选择器的元素，兼容性： IE7+
### 选择器优先级

一般而言，选择器越特殊，它的优先级越高。也就是选择器指向的越准确，它的优先级就越高。

用1表示派生选择器的优先级
用10表示类选择器的优先级
用100标示ID选择器的优先级

> 如果重复定义一个属性，则会 样式覆盖。 .classA{ color:blue;} .classB{ color:red;}// red
## display: none;与visibility: hidden;的区别
都让元素不可见
区别：
1 display:none;会让元素完全从渲染树中消失，渲染的时候不占据任何空间；visibility: hidden;不会让元素从渲染树消失，渲染师元素继续占据空间，只是内容不可见
2 display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示；visibility: hidden;是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式
3 修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。
4 读屏器不会读取display: none;元素内容；会读取visibility: hidden;元素内容
### CSS中可以通过哪些属性定义，使得一个DOM元素不显示在浏览器可视范围内？　　
除了以上两种，还可以 设置宽高为0；设置透明度为0；设置z-index位置在-1000

## 超链接访问过后hover样式就不出现的问题是什么？如何解决？

被点击访问过的超链接样式不在具有hover和active了,解决方法是改变CSS属性的排列顺序: L-V-H-A（link,visited,hover,active

## 什么是Css Hack？ie6,7,8的hack分别是什么？

针对不同的浏览器写不同的CSS code的过程，就是CSS hack。

```
#test       {   
        width:300px;   
        height:300px;   
          
        background-color:blue;      /*firefox*/
        background-color:red\9;      /*all ie*/
        background-color:yellow\0;    /*ie8*/
        +background-color:pink;        /*ie7*/
        _background-color:orange;       /*ie6*/    }  
        :root #test { background-color:purple\9; }  /*ie9*/
    @media all and (min-width:0px){ #test {background-color:black\0;} }  /*opera*/
    @media screen and (-webkit-min-device-pixel-ratio:0){ #test {background-color:gray;} 
    }       /*chrome and safari*/
    
```
## css sprite
概念：将多个小图片拼接到一个图片中。通过background-position和元素尺寸调节需要显示的背景图案。

优点：

减少HTTP请求数，极大地提高页面加载速度
增加图片信息重复度，提高压缩比，减少图片大小
更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现
缺点：

图片合并麻烦
维护麻烦，修改一个图片可能需要从新布局整个图片，样式

## link与@import的区别
link是HTML方式， @import是CSS方式
link最大限度支持并行下载，@import过多嵌套导致串行下载，出现FOUC
link可以通过rel="alternate stylesheet"指定候选样式
浏览器对link支持早于@import，可以使用@import对老浏览器隐藏样式
@import必须在样式规则之前，可以在css文件中引用其他文件
总体来说：link优于@import

## display: block;和display: inline;的区别
block元素特点：

1. 处于常规流中时，如果width没有设置，会自动填充满父容器 
2. 可以应用margin/padding 
3. 在没有设置高度的情况下会扩展高度以包含常规流中的子元素 
4. 处于常规流中时布局时在前后元素位置之间（独占一个水平空间） 
5. 忽略vertical-align

inline元素特点

1. 水平方向上根据direction依次布局 
2. 不会在元素前后进行换行 
3. 受white-space控制 
4. margin/padding在竖直方向上无效，水平方向上有效 
5. width/height属性对非替换行内元素无效，宽度由元素内容决定 
6. 非替换行内元素的行框高由line-height确定，替换行内元素的行框高由height,margin,padding,border决定 
7. 浮动或绝对定位时会转换为block 
8. vertical-align属性生效

###浏览器有默认的天生inline-block元素（拥有内在尺寸，可设置高宽，但不会自动换行），有哪些？

<input> 、<img> 、<button> 、<textarea> 、<label>

## 媒体查询的原理是什么
**媒体查询包含一个可选的媒体类型和**
满足CSS3规范的条件下，包含零个或多个表达式，这些表达式描述了媒体特征，最终会被解析为true或false。如果媒体查询中**指定的媒体类型匹配展示文档所使用的设备类型**，并且所有的表达式的值都是true，那么该媒体查询的结果为true.

## css渲染规则
从右到左的渲染
```
.nav h3 a{font-size: 14px;}
```
首先找到所有的a，沿着a的父元素查找h3，然后再沿着h3，查找.nav。中途找到了符合匹配规则的节点就加入结果集。如果找到根元素html都没有匹配，则不再遍历这条路径，从下一个a开始重复这个查找匹配（只要页面上有多个最右节点为a）。

## px, em, rem
px是固定的。
em的值并不是固定的；em会继承父级元素的字体大小。
rem 相对的是HTML根元素的大小。
## 什么是FOUC?如何避免
Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。解决方法：把样式表放到文档的head

## 外边距折叠(collapsing margins)
毗邻的两个或多个margin会合并成一个margin，叫做外边距折叠。规则如下：

1.两个或多个毗邻的普通流中的块元素垂直方向上的margin会折叠
2.浮动元素/inline-block元素/绝对定位元素的margin不会和垂直方向上的其他元素的margin折叠
3.创建了块级格式化上下文的元素，不会和它的子元素发生margin折叠
4.元素自身的margin-bottom和margin-top相邻时也会折叠

## rgba()和opacity的透明效果有什么不同？

　rgba()和opacity都能实现透明效果，但最大的不同是opacity作用于元素，以及元素内的所有内容的透明度，

　而rgba()只作用于元素的颜色或其背景色

## css中可以让文字在垂直和水平方向上重叠的两个属性是什么？

　垂直方向：line-height

　水平方向：letter-spacing
> letter-spacing的妙用: 可以用于消除inline-block元素间的换行符空格间隙问题。

## 如何垂直居中一个浮动元素
```
// 方法一：已知元素的高宽
 2 
 3 #div1{
 4     background-color:#6699FF;
 5     width:200px;
 6     height:200px;
 7 
 8     position: absolute;        //父元素需要相对定位
 9     top: 50%;
10     left: 50%;
11     margin-top:-100px ;   //二分之一的height，width
12     margin-left: -100px;
13     }
14 
15 //方法二:
16 
17   #div1{
18     width: 200px;
19     height: 200px;
20     background-color: #6699FF;
21 
22     margin:auto;
23     position: absolute;        //父元素需要相对定位
24     left: 0;
25     top: 0;
26     right: 0;
27     bottom: 0;
28     }
```
### 如何垂直居中一个\<img>\
```
#container     //<img>的容器设置如下
{
    display:table-cell;
    text-align:center;
    vertical-align:middle;
}
```