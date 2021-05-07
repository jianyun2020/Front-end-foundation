# 基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。 

*注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。*

![](../images/flex01.png)

容器默认存在两根轴：

- 水平的主轴(`main axis`)
- 垂直的交叉轴(`cross axis`)

主轴的开始位置（与边框的交叉点）叫做(`main start`)，结束位置叫做(`main end`)

交叉轴的开始位置叫做(`cross start`)，结束位置叫做(`cross end`)

项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`

# 容器的属性

- `flex-direction`
- `flex-wrap`
- `flex-flow`
- `justify-content`
- `align-items`
- `align-content`

## flex-direction

`flex-direction`属性决定主轴的方向（即项目排列的方向）

属性值有以下4个：

- row(默认值)：主轴为水平方向，起点在左端
- row-reverse：主轴为水平方向，起点在右端
- column：主轴为垂直方向，起点在上沿
- column-reverse：主轴为垂直方向，起点在下沿