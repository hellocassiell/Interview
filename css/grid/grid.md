使用display属性来定义一个网格容器，一旦启用网格容器，它的所有子元素都进入grid文档流，称为网格子项。
```
display: grid | inline-grid | subgrid
```
- grid：定义一个块级的网格容器
- inline-grid：定义一个内联的网格容器
- subgrid：定义一个继承其父级网格容器的行和列的大小的网格容器，它是其父级网格容器的一个子项。
注意：column, float, clear和vertical-align对网格容器没有效果。