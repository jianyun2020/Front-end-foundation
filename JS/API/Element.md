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