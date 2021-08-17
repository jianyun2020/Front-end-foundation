- [简介](#简介)
- [属性](#属性)
  - [classList](#classlist)
    - [示例](#示例)
  - [className](#classname)
    - [语法](#语法)
  - [innerHTML](#innerhtml)
  - [outerHTML](#outerhtml)
  - [clientHeight](#clientheight)
  - [clientWidth](#clientwidth)
  - [clientLeft](#clientleft)
- [方法](#方法)
  - [closest()](#closest)
    - [语法](#语法-1)
    - [参数](#参数)
    - [返回值](#返回值)
    - [示例](#示例-1)
  - [prepend()](#prepend)
    - [语法](#语法-2)
    - [参数](#参数-1)
    - [返回值](#返回值-1)
    - [示例](#示例-2)
  - [append()](#append)
    - [语法](#语法-3)
    - [参数](#参数-2)

# 简介

Element 是一个通用性非常强的基类，所有 Document 对象下的对象都继承自它。这个接口描述了所有相同种类的元素所普遍具有的方法和属性。一些接口继承自 Element 并且增加了一些额外功能的接口描述了具体的行为。例如， HTMLElement 接口是所有 HTML 元素的基本接口，而 SVGElement 接口是所有 SVG 元素的基础。大多数功能是在这个类的更深层级（hierarchy）的接口中被进一步制定的。

在 Web 平台的领域以外的语言，比如 XUL，通过 XULElement 接口，同样也实现了 Element 接口。

# 属性

> 所有属性继承自它的祖先接口`Node`，并且扩展了`Node`的父接口`EventTarget`

## classList

Element.classList是一个只读属性，返回一个元素的类属性的实时DOMTokenList集合。

相比将element.className作为以空格分隔的字符串来使用，classList是一种更方便的访问元素的类列表的方法。

*可用`DOMTokenList`的`add()`方法和`remove()`方法修改*

### 示例

```js
const div = document.createElement("div");

div.className = "foo";

console.log(div.outerHTML); // <div class="foo"></div>

div.classList.remove("foo");
div.classList.add("bar");

console.log(div.outerHTML); // <div class="bar"></div>

// 如果visible类值已存在，则移除它，否则添加它
div.classList.toggle("visible");

// add/remove visible，当i<10时
div.classList.toggle("visible", i < 10);

console.log(div.classList.contains("bar")); // true

// 添加或移除多个类值
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// 使用展开语法添加或移除多个类值
const cls = ["foo", "bar"];
div.classList.add(...cls);
div.classList.remove(...cls);

// 将类值"foo"替换成"bar"
div.classList.replace("foo", "bar");
```

## className

获取或设置指定元素的class属性的值。

### 语法

```js
let cName = elementNodeReference.className;

elementNodeReference.className = cName;
```

*cName是一个字符串变量，表示当前元素的class属性的值，可以是由空格分隔的多个class属性值。*

## innerHTML

设置或获取HTML语法表示的元素的后代

## outerHTML

获取描述元素（包括其后代）的序列化HTML片段。它也可以设置为用从给定字符串解析的节点替换元素。

要仅获取元素内容的HTML表示形成或替换元素的内容，请使用`innerHTML`属性。


## clientHeight

只读属性，对于没有定义CSS或者内联布局盒子的元素为0，否则，它是元素内部的高度（单位像素），包含内边距，但不包括水平滚动条、边框和外边距。

clientHeight = CSS height + CSS padding - 水平滚动条高度（如果存在）

## clientWidth

内联元素以及没有CSS样式的元素的clientWidth属性值为0。Element.clientWidth属性表示元素的内部宽度，以像素计。该属性包括内边距padding,但不包括边框border、外边距margin和垂直滚动条

## clientLeft

只读属性，表示一个元素的左边框的宽度，以像素表示。如果元素的文本方向是从右向左，并且由于内容溢出导致左边出现了一个垂直滚动条，则该属性包括滚动条的宽度。clientLeft 不包括左外边距和左内边距。

# 方法

## closest()

Element.closest()方法用来获取：匹配特定选择器且离当前元素最近的祖先元素（也可以是当前元素本身）。如果匹配不到，则返回null。

### 语法

```js
const closeetElement = targetElement.closest(selector);
```

### 参数

- selectors是指定的选择器，比如`p:hover, .toto + q`。

### 返回值

- elt是查询到的祖先元素，也可能是null。

### 示例

```html
<article>
  <div id="div-01">
    		<article>
			<div id="div-01">
				Here is div-01
				<div id="div-02">
					Here is div-02
					<div id="div-03">
						Here is div-03
					</div>
				</div>
			</div>
		</article>
  </div>
</article>
```

```js
const el = document.getElementById('div-03');

const r1 = el.closest('#div-02'); // 返回id为div-02的那个元素

const r2 = el.closest('div div'); // 返回最近的拥有div祖先元素的div祖先元素，这里是div-03元素本身

const r3 = el.closest('article > div'); // 返回最近的拥有父元素article的div祖元素，这里是div-01元素本身

const r4 = el.closest(':not(div)'); // 返回最近的非div祖先元素，这里是最外层的article
```

## prepend()

Element.prepend()方法可以在父节点的第一个子节点之前插入一系列Node对象或者DOMString对象。DOMString会被当做Text节点对待（也就是说插入的不是HTML代码）。

### 语法

```js
Element.prepend((Node or DOMString)... nodes);
```

### 参数

- nodes：要插入的一系列Node或者DOMString。

### 返回值

undefined

### 示例

- 在父节点的第一个子节点前插入节点

```js
const parent = document.createElement("div");
const p = document.createElement("p");
const span = document.createElement("span");

parent.append(p);
parent.prepend(span);

console.log(parent.childNodes); // NodeList [ <span>, <p> ]
```

- 在文字前面插入文字

```js
const parent = document.createElement("div");
parent.append("Some text");
parent.prepend("Headline: ");

console.log(parent.textContent); // Headline: Some text
```

- 同时在尾部插入节点和文字

```js
const parent = document.createElement("div");
const p = document.createElement("p");

parent.prepend("Some text", p);

console.log(parent.childNodes); // NodeList [ #text "Some text", <p>]
```

## append()

Element.append()方法在Element的最后以个子节点之后插入一组Node对象或DOMString对象。被插入的DOMString对象等价为Text节点。

与Node.appendChild()的差异：

- Element.append()允许追加DOMString对象，而Node.appendChild()只接受Node对象。
- Element.append()没有返回值，而Node.appendChild()返回追加的Node对象。
- Element.append()可以追加多个节点和字符串，而Node.appendChild()只能追加一个节点。

### 语法

```js
Element.append((Node or DOMString)... nodes);
```

### 参数

- nodes:一组要插入的Node或DOMString对象。


