1. 介绍一下标准的CSS的盒子模型？与低版本IE的盒子模型有什么不同的？

标准盒子模型：宽度=内容的宽度(content) + padding + border + margin
低版本IE盒子模型：宽度=内容宽度(content+padding+border) + margin

2. box-sizing属性？

用来控制元素的盒子模型的解析模式，默认为content-box

content-box：W3C的标准盒子模型，设置元素的height/width属性指的是border + padding + content部分的高/宽

boder-box：IE传统盒子模型。设置元素的height/width属性指的是content部分的高/宽

3. CSS选择器有哪些？哪些属性可以继承？

css选择器：

|分类|举例|描述|
|-|-|-|
|通配符选择器|`* {}`|通过`*`选择页面里面的所有元素|
|ID选择器|`#idName {}`|选择id="xxx"的DOM元素|
|类选择器|`.className {}`|选择class="xxx"的DOM元素|
|标签选择器|`div {}`|选择某一类标签|
|属性选择器|`a[attr] or a[attr=xxx]`|通过标签的属性选择元素|
|组合选择器：|||
|>后代选择器|`.className p`|选择后代中所有匹配的元素|
|>子元素选择器|`.className > p`|只找子元素，不会找子元素的子元素|
|>相邻兄弟选择器|`div + p`|匹配div后面的第一个p元素（相邻）|
|>通用兄弟选择器|`div ~ p`|匹配div后面的所有p元素|
|>交集选择器|`.className.active`|匹配同时包含`className和active`类名的元素|
|>并集选择器|`h1, h2, p`|为多个元素设置相同的样式|
|伪类和伪元素选择器|||
|>标记状态的伪类|`:link`|选取未访问过的超链接|
||`:visited`|选取访问过的超链接|
||`:hover`|选取鼠标悬浮的元素|
||`:active`|选取鼠标点击的元素|
||`:focus`|选取获得焦点的元素|
|>筛选功能的伪类|`:empty`|选取没有子元素的元素如(`<div></div>`|
||`:checked`|选取勾选状态下的input元素，只对radio和checkbox有效|
||`:disabled`|选取禁用的表单元素|
||`:first-child`|选取当前选择器下的第一个元素|
||`:last-child`|选取当前选择器下的最后一个元素|
||`:nth-child(an+b)`|选取指定位置的元素,参数支持an+b的形势.比如 li:nth(2n+1),就可以选取li元素序号是2的整数倍+1的所有元素,也就是1,3,5,7,9序号的li元素|
||`:nth-last-child`|和上面类似,不过从后面选取|
||`:only-child`|选取元素唯一的子元素,如果元素的父元素只有它一个子元素就会生效,如果还有其他的兄弟元素,则不生效|
||`:only-of-type`|选取唯一的某个元素类型。如果元素的父元素只有它一个当前类型的子元素就会生效。|
|>伪元素选择器||伪元素选择器并不是真实的DOM元素|
||`::first-line`|为元素的第一行使用样式|
||`::first-letter`|为某个元素的首字母或第一个文字使用样式|
||`::before`|在某个元素之前插入内容|
||`::after `|在某个元素之后插入内容|
||`::selection`|对光标选中的元素添加样式|

*注意：如果同时使用了 befor 和first-letter. 第一个内容要从before中算起,如果before 中第一个为非文本内容,那first-letter也会作用到这个非文本内容上,但不会生效。在CSS3 中规定, 伪类用一个冒号 (:) 表示, 伪元素用两个冒号 (::)来表示*

可继承的属性：font-size, font-family, color

不可继承的属性：border, padding, margin, width, height

优先级(就近原则)：!important > [id > class > tag]

!important 比内联优先级高

4. CSS优先级算法是如何计算的？

《CSS REFACTORING》 中提到了算法的过程：

> A specificity is determined by plugging numbers into (a, b, c, d):
> 1. If the styles are applied via the style attribute, a=1; otherwise, a=0.
> 2. b is equal to the number of ID selectors present.
> 3. c is equal to the number of class selectors, attribute selectors, and pseudoclasses present.
> 4. d is equal to the number of type selectors and pseudoelements present.

简单来说就是，优先级是由 a, b, c, d 的值来决定的，其中它们的值计算规则如下：

1. 如果存在内联样式，那么 a = 1, 否则 a = 0;
2. b 的值等于 ID选择器 出现的次数;
3. c 的值等于 类选择器 和 属性选择器 和 伪类 出现的总次数;
4. d 的值等于 标签选择器 和 伪元素 出现的总次数 。

例如：

`#nav-global > ul > li > a.nav-link`

通过上述算法计算，依次求出a, b, c, d的值:

1. 没有内联样式：a = 0
2. ID选择器共出现1次，b = 1
3. 类选择器出现1次，属性选择器出现0次，伪类选择器出现0次，c = (1 + 0 + 0)
4. 标签选择器出现3次，d = 3

简记为：(0, 1, 1, 3)

如果使用了`!important`，则优先级最高，此为特殊情况。

5. CSS3新增伪类有那些?

- p:first-of-type：选择属于其父元素的首个元素
- p:last-of-type：选择属于其父元素的最后一个元素
- p:only-of-type：选择属于其父元素的唯一子元素
- p:only-child：选择属于其父元素的唯一子元素
- p:nth-child(2)：选择属于其父元素的第二个子元素
- :enabled, :disabled：表单控件的禁用状态
- :checked：单选框或复选框被选中

6. 