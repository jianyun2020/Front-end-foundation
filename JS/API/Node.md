- [简介](#简介)
- [nextSibling](#nextsibling)
- [firstChild](#firstchild)


# 简介

Node 是一个接口，各种类型的 DOM API 对象会从这个接口继承。它允许我们使用相似的方式对待这些不同类型的对象；比如, 继承同一组方法，或者用同样的方式测试。

以下接口都从 Node 继承其方法和属性：

- Document
- Element
- Attr
- CharacterData
- ProcessingInstruction
- DocumentFragment
- DocumentType

在方法和属性不相关的特定情况下，这些接口可能返回null。

# nextSibling

Node.nextSibling是一个只读属性，返回其父节点的childNodes列表中紧跟在其后面的节点，如果指定的节点为最后一个节点，则返回null。

> Gecko内核的浏览器会在源代码中标签内部有空白符的地方插入一个文本结点到文档中.因此,使用诸如 Node.firstChild 和 Node.previousSibling 之类的方法可能会引用到一个空白符文本节点, 而不是使用者所预期得到的节点.


# firstChild

Node.firstChild 只读属性返回树中节点的第一个子节点，如果节点是无子节点，则返回 null。