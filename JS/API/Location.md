- [属性](#属性)
  - [href](#href)
  - [protocol](#protocol)

Location 接口表示其链接到的对象的位置（URL）。所做的修改反映在与之相关的对象上。 Document 和 Window 接口都有这样一个链接的Location，分别通过 Document.location和Window.location 访问。

# 属性

## href

包含整个URL的一个DOMString

```js
location.href // https://developer.mozilla.org/zh-CN/docs/Web/API/Location
```

Location 接口的 href 属性是一个字符串化转换器(stringifier), 返回一个包含了完整 URL 的 USVString 值, 且允许 href 的更新.

例：

```js
// 假设文档中包含标签： <a id="myAnchor" href="https://developer.mozilla.org/en-US/Location/href">
const anchor = document.getElementById("myAnchor");
const result = anchor.href; // 返回: 'https://developer.mozilla.org/en-US/Location/href'

```

## protocol

包含URL对应协议的一个DOMString， 最后有一个":"

Location接口的protocol属性是一个USVString，表示URL的协议方案，包括最后的':'

例：

```js
// Let's an <a id="myAnchor" href="https://developer.mozilla.org/en-US/Location.protocol"> element be in the document
const anchor = document.getElementById("myAnchor");
const result = anchor.protocol; // Returns:'https:'
```