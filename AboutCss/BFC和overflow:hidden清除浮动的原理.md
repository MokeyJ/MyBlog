# overflow:hidden清除浮动的原理
我们都知道"overflow:hidden"可以溢出隐藏，即当内容元素的高度大于其包含块的高度时，设置该属性即可把内容区域超出来的部分隐藏，使内容区域完全包含在该包含块中。

然而"overflow:hidden"还有另外一个特殊的用途，那就是清除包含块内子元素的浮动。可是原因是什么呢？在解释这个问题之前，我们先了解一下BFC的概念。

## BFC
BFC（Block Formatting Context），块级格式化上下文，它规定了内部的块级元素的布局方式，默认情况下只有根元素（即body）一个块级上下文。

#### BFC布局规则

+ 内部的块级元素会在垂直方向，一个接一个地放置；
+ 块级元素垂直方向的距离由margin决定。**属于同一个BFC的两个相邻的块级元素会发生margin合并，不属于同一个BFC的两个相邻的块级元素不会发生margin合并；**
+ 每个元素的margin box的左边，与包含border box的左边相接触（对于从左往右的格式化，否则相反）。即使存在浮动也是如此；
+ BFC的区域不会与float box重叠；
+ **BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素；外面的元素也不会影响到容器里面的子元素；**
+ **计算BFC的高度时，浮动元素也参与计算。**

#### 创建一个BFC
+ 首先我们要知道怎样创建BFC。一个BFC可以被显式触发，只需满足以下条件之一：
+ float的值不为none；
+ overflow的值不为visible；
+ position的值为fixed / absolute；
+ display的值为table-cell / table-caption / inline-block / flex / inline-flex。

#### BFC的应用
###### 消除margin合并
在margin合并这篇博客中，我描述了相邻兄弟元素、父元素与第一个和最后一个子元素、空块元素的margin合并情况。那么对于发生margin合并的元素，我们怎样消除margin合并？

对于父子元素，我们可以通过设置padding、border、inline content、height、min-height、max-height等属性来消除；但是相邻的兄弟元素之间必出现margin合并，这时如果想要消除margin合并，又该怎么办？

我们首先要搞清楚为什么会发生margin合并。这些元素（包括兄弟、父子元素等）之间之所以会发生margin合并，是因为它们属于同一个BFC。所以，我们就知道怎么办了，只要让它们不属于同一个BFC不就可以了？

###### 包含浮动子元素
这也是我们今天的主要议题——为什么"overflow:hidden"能清除浮动的影响。

我们经常会在父元素里设置某个子元素浮动。浮动后，子元素脱离了文档流，使得父元素无法包住这个浮动的子元素。我们通常在父元素上设置一个clearfix的伪元素来清除浮动；同样，我们可以利用BFC可以包含浮动这一特性来清除浮动。

当给父级设置"overflow:hidden"时，实际上创建了一个超级属性BFC，此超级属性反过来决定了"height:auto"是如何计算的。在“BFC布局规则”中提到：计算BFC的高度时，浮动元素也参与计算。因此，父元素在计算其高度时，加入了浮动元素的高度，“顺便”达成了清除浮动的目标，所以父元素就包裹住了子元素。

除了给.parent设置"overflow:hidden"，我们还可以设置"display:inline-block"、"position:absolute"、"float:left"等方式来创建一个BFC，从而达到包裹浮动子元素的效果（具体使用哪种方法要看项目需求）

