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
