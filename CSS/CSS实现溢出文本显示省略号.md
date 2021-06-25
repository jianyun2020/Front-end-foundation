# 单行文本

参考链接：
[掘金-pekonchan](https://juejin.cn/post/6844903817536897032)
[Github-happylindz](https://github.com/happylindz/blog/issues/12)

```css
div {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

# 多行文本

## 通过`-webkit-line-clamp`实现

```css
div {
  overflow: hidden;
  display: -webkit-box; /* 将对象作为弹性伸缩盒子模型显示 */
  -webkit-line-clamp: 2; /* 将块容器中的内容限制为指定的行数. */
  -webkit-box-orient: vertical; /* 设置或检索伸缩盒对象的子元素的排列方式 */
}
```

## 通过绝对定位实现

```css
div {
  position: relative;
  line-height: 1.2em; /* line-height和height要相互配合，显示多少行省略，就是line-height的多少倍数。 */
  max-height: 3.6em;
  /* margin-left: -1em; */  /* 看需求设置，一般为padding-right的负值 */
  padding-right: 1em; /* 省略号大概占1em的空间 */
  text-align: justify;
  overflow: hidden;
  background: #fff;
}

/* 省略号 */
div:before {
  position: absolute;
  right: 0;
  bottom: 0;
  content: '...'
}

/* 由于省略号会默认一直显示，因此用和文字背景相同的颜色来盖住省略号 */
/* 思路： 用于挡住省略号的方块也是绝对定位，靠右定为，right: 0，但是bottom值就不要设置了，如果不设置的话，该方块会跟着文本内容的实际高度移动，而不是max-height的高度。这样的话，当不需要省略时（即不超过max-height）时，就刚好是bottom: 0的情况，就会挡住省略号。当要进行省略时（即超过max-height）就会挡不住省略号了，它自己也会被overflow: hidden给隐藏掉了。 */
div:after {
  position: absolute;
  right: 0;
  width: 1em; /* 宽高写死1em就好，因为省略号大概就是占用1em的空间，用来遮挡住省略号，也基本上跟wrap的padding-right一致 */
  height: 1.2em; /* 与wrap的行高实际值保持一致 */
  content: '',
  background-color: #fff; /* 要跟所在背景颜色一致才能遮挡住省略号后觉得没异样 */
}
```

## 通过float布局实现

```html
<div class="wrap">
    <span class="text">
       /*文字*/ 
    </span>
</div>

```

```css
.wrap {
    /*需要定高*/
    height: 100px;
    /*用来设置显示多少行才省略，值一般为wrap的height值/行数求得，但是这个行数会受到字体大小的限制*/
    /*字体太大了，设置显示很多行也会很丑，都挤一块了，所以这个实际值，要看具体需求和实践*/
    line-height: 25px;
    /*加上此属性显示效果更佳，就算部分浏览器不支持也影响不大*/
    text-align: justify;
    overflow: hidden;
    background: #fff;
}

.wrap:before {
    float: left;
    /*这个值可以随意设定，不论单位还是什么*/
    width: 1em;
    height: 100%;
    content: '';
}

.wrap:after {
    float: right;
    /*大小随意，设置em单位最好，可随字体大小变化而自适应*/
    /*如果要采用以下渐变效果，那么这个值要大于before里的width值效果会比较好点*/
	/*值越大，渐变的效果越明显影响的范围越大。*/
    width: 2.5em;
    /*与父元素wrap的行高实际px值一样*/
    height: 25px;
    /*此值要跟自身宽度一样，取负值*/
    margin-left: -2.5em;
    /*此值要跟before宽度一样*/
    padding-right: 1em;
    content: '...';
    text-align: right;
    /*这里开始利用在float布局的基础上进行定位移动了*/
    position: relative;
    /*与父元素wrap的行高实际值一样，取负值*/
    top: -25px;
    left: 100%;
    /*设置渐变效果是为了省略号和内容衔接得自然点，没那么突兀，要注意要跟文字所在的背景的颜色搭配（把white替换成背景色）*/
    background: #fff;
    background: -webkit-gradient(linear, left top, right top, from(rgba(255, 255, 255, 0)), to(white), color-stop(50%, white));
    background: -moz-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
    background: -o-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
    background: -ms-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
    background: linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
}

.wrap .text {
    float: right;
    /*该值要等于wrap:before的width值*/
    margin-left: -1em;
    width: 100%;
}

```
