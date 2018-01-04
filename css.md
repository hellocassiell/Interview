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
1 *通用选择器：选择所有元素，不参与计算优先级，兼容性IE6+
2 #X id选择器：选择id值为X的元素，兼容性：IE6+
3 .X 类选择器： 选择class包含X的元素，兼容性：IE6+
4 X Y后代选择器： 选择满足X选择器的后代节点中满足Y选择器的元素，兼容性：IE6+
5 X 元素选择器： 选择标所有签为X的元素，兼容性：IE6+
6 :link，：visited，：focus，：hover，：active链接状态： 选择特定状态的链接元素，顺序LoVe HAte，兼容性: IE4+
7 X + Y直接兄弟选择器：在X之后第一个兄弟节点中选择满足Y选择器的元素，兼容性： IE7+
8 X > Y子选择器： 选择X的子元素中满足Y选择器的元素，兼容性： IE7+
9 X ~ Y兄弟： 选择X之后所有兄弟节点中满足Y选择器的元素，兼容性： IE7+

## display: none;与visibility: hidden;的区别
都让元素不可见
区别：
1 display:none;会让元素完全从渲染树中消失，渲染的时候不占据任何空间；visibility: hidden;不会让元素从渲染树消失，渲染师元素继续占据空间，只是内容不可见
2 display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示；visibility: hidden;是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式
3 修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。
4 读屏器不会读取display: none;元素内容；会读取visibility: hidden;元素内容

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

1.处于常规流中时，如果width没有设置，会自动填充满父容器 2.可以应用margin/padding 3.在没有设置高度的情况下会扩展高度以包含常规流中的子元素 4.处于常规流中时布局时在前后元素位置之间（独占一个水平空间） 5.忽略vertical-align

inline元素特点

1.水平方向上根据direction依次布局 2.不会在元素前后进行换行 3.受white-space控制 4.margin/padding在竖直方向上无效，水平方向上有效 5.width/height属性对非替换行内元素无效，宽度由元素内容决定 6.非替换行内元素的行框高由line-height确定，替换行内元素的行框高由height,margin,padding,border决定 6.浮动或绝对定位时会转换为block 7.vertical-align属性生效

##  PNG,GIF,JPG的区别及如何选
参考资料： 选择正确的图片格式 GIF:

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


## 媒体查询的原理是什么
**媒体查询包含一个可选的媒体类型和**
满足CSS3规范的条件下，包含零个或多个表达式，这些表达式描述了媒体特征，最终会被解析为true或false。如果媒体查询中**指定的媒体类型匹配展示文档所使用的设备类型**，并且所有的表达式的值都是true，那么该媒体查询的结果为true.

## css渲染规则
从右到左的渲染
```
.nav h3 a{font-size: 14px;}
```
首先找到所有的a，沿着a的父元素查找h3，然后再沿着h3，查找.nav。中途找到了符合匹配规则的节点就加入结果集。如果找到根元素html都没有匹配，则不再遍历这条路径，从下一个a开始重复这个查找匹配（只要页面上有多个最右节点为a）。