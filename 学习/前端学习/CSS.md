## 语义化

裸奔的css，指的是那些使用最恰当的HTML元素进行标记的内容，同时让浏览器的爬虫和机器很好地解析，方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页

如：header 、footer、nav、aside、section、article、strong、em、h1等

利用搜索引擎搜索，爬虫对页面的爬取，利于识别、阅读，方便其他设备解析（如移动设备、盲人阅读器等）

## 块元素

独占一行

设置width、height等属性

宽度默认是它容器的100%，除非设定一个宽度

他可以容纳内联元素和其他块元素

如：div、h1、form、hr、p、ul、ol、table 等

## 内联元素

和其他内联元素都在同一行

内联元素只能容纳文本或者其他内联元素

宽度就是它的文字和图片的宽度，不可改变

如：span、a、lable、input、img、u、strong、i、b、em等

## 盒子模型

盒子由content、padding、border、margin组成

标准：宽度=内容的宽度（content）+border+padding+margin

低版：宽度=内容宽度（content+border+padding）+margin

设置宽高，都是在给内容区设置宽高

## display和visibility的区别

display:none;元素不可见，并且不为其保留相应的位置

visibility:hidden;元素不可见，但仍然为其保留相应的空间

## css浮动float

设置float属性，默认在元素上加了一个display：block；宽高默认文本内容宽高

浮动方向决定紧贴父元素哪一侧，撑不起父元素的宽度和高度

## 清除浮动

在浮动元素后面新增一个块级元素，设置clear：both；此时可撑起父元素的高度，宽度不用关注

父元素使用display：flex；相当于在此父元素的子元素加上display：inline-block；强行清除float、clear、opsition

## css选择器

ID选择器 #

类选择器 .

标签选择器

伪类选择器 hover active fcous等

子选择器  >

后代选择器

全局选择器 *

兄弟 +

等

## css选择器优先级

1、在属性值后面加上 ！important

2、内联 1000

3、ID选择器 100

4、类选择器 10

5、标签选择器 1

6、通配选择器 *

7、浏览器自定义或继承

## CSS浏览器前缀兼容写法:

-moz-     /* 火狐等使用Mozilla浏览器引擎的浏览器 */

-webkit-  /* Safari, 谷歌浏览器等使用Webkit引擎的浏览器 */

-o-       /* Opera浏览器(早期) */

-ms-      /* Internet Explorer (不一定) */


## 弹性布局

父级属性：display:flex;

flex-direction 属性决定主轴的方向（即项目的排列方向）。

	row（默认值）：主轴为水平方向，起点在左端。
	
	row-reverse：主轴为水平方向，起点在右端。
	
	column：主轴为垂直方向，起点在上沿。
	
	column-reverse：主轴为垂直方向，起点在下沿。
	
	flex-wrap 默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
	
	nowrap（默认）：不换行。
	
	wrap：换行，第一行在上方。
	
	wrap-reverse：换行，第一行在下方。
	
	flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

justify-content属性定义了项目在主轴上的对齐方式。

	flex-start（默认值）：左对齐
	
	flex-end：右对齐
	
	center： 居中
	
	space-between：两端对齐，项目之间的间隔都相等。
	
	space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

align-items属性定义项目在交叉轴上如何对齐。

	flex-start：交叉轴的起点对齐。
	
	flex-end：交叉轴的终点对齐。
	
	center：交叉轴的中点对齐。
	
	baseline: 项目的第一行文字的基线对齐。
	
	stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

	flex-start：与交叉轴的起点对齐。
	
	flex-end：与交叉轴的终点对齐。
	
	center：与交叉轴的中点对齐。
	
	space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
	
	space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
	
	stretch（默认值）：轴线占满整个交叉轴。

项目的属性：

order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。

flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。