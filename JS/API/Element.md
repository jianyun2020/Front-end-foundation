- [closest()](#closest)
  - [语法](#语法)
  - [参数](#参数)
  - [返回值](#返回值)
  - [示例](#示例)
- [prepend()](#prepend)
  - [语法](#语法-1)
  - [参数](#参数-1)
  - [返回值](#返回值-1)
  - [示例](#示例-1)
- [append()](#append)
  - [语法](#语法-2)
  - [参数](#参数-2)

# closest()

Element.closest()方法用来获取：匹配特定选择器且离当前元素最近的祖先元素（也可以是当前元素本身）。如果匹配不到，则返回null。

## 语法

```js
const closeetElement = targetElement.closest(selector);
```

## 参数

- selectors是指定的选择器，比如`p:hover, .toto + q`。

## 返回值

- elt是查询到的祖先元素，也可能是null。

## 示例

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

# prepend()

Element.prepend()方法可以在父节点的第一个子节点之前插入一系列Node对象或者DOMString对象。DOMString会被当做Text节点对待（也就是说插入的不是HTML代码）。

## 语法

```js
Element.prepend((Node or DOMString)... nodes);
```

## 参数

- nodes：要插入的一系列Node或者DOMString。

## 返回值

undefined

## 示例

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

# append()

Element.append()方法在Element的最后以个子节点之后插入一组Node对象或DOMString对象。被插入的DOMString对象等价为Text节点。

与Node.appendChild()的差异：

- Element.append()允许追加DOMString对象，而Node.appendChild()只接受Node对象。
- Element.append()没有返回值，而Node.appendChild()返回追加的Node对象。
- Element.append()可以追加多个节点和字符串，而Node.appendChild()只能追加一个节点。

## 语法

```js
Element.append((Node or DOMString)... nodes);
```

## 参数

- nodes:一组要插入的Node或DOMString对象。


