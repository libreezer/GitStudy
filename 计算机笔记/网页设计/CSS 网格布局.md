网格是一组相交的水平线和垂直线，它定义了网格的列和行。
CSS 提供了一个基于网格的布局系统，带有行和列，可以让我们更轻松地设计网页，而无需使用浮动和定位。
# display 属性
当一个 HTML 元素将 display 属性设置为 grid 或 inline-grid 后，它就变成了一个网格容器，这个元素的所有直系子元素将成为网格元素。
```
.grid-container{
	display: grid;
}
```
# 网格轨道
我们通过 `grid-template-columns` 和 `grid-template-rows` 属性来定义网格中的行和列。
这些属性定义了网格的轨道，一个网格轨道就是网格中任意两条线之间的空间。
<u>就是每个空间的大小，为避免复杂使用repeat()函数</u>

# 网格间距
网格间距（Column Gap）指的是两个网格单元之间的网格横向间距或网格纵向间距。
>[! ] Tips:
>您可以使用以下属性来调整间隙大小：
>- grid-column-gap
>- grid-row-gap
>- grid-gap

