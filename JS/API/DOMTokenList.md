- [简介](#简介)

# 简介

DOMTokenList接口表示一组空格分隔的标记。如由`Element.classList`、`HTMLLinkElement.relList`、`HTMLAnchorElement.relList`或`HTMLAreaElement.relList`返回的一组值。它和JavaScript `Array`对象一样，索引从0开始。DOMTokenList总是区分大小写。

# 属性

## length

一个整数，表示存储在该对象里值的个数。

# 方法

## add()

将给定的标记添加到列表中。

### 语法

```js
tokenList.add(token1[, token2[, ...tokenN]]);
```

### 参数

- tokenN：一个DOMString，表示要添加到列表里的标记。

### 返回值

undefined

## remove()

移除指定标记

### 语法

```js
tokenList.remove(token1[, token2[, ...]]);
```

### 参数

- tokenN：表示要从列表移除的一个DOMString。如果列表中不存在改字符串，不会出错也没有任何变化。

### 返回值

undefined

## toggle()

从列表中删除一个给定的标记并返回false；如果标记不存在，则添加并且函数返回true。

### 语法

```js
tokenList.toggle(token, force);
```

### 参数

- token：想要探查并切换的`DOMString`
- force`可选`：`Boolean`,设置后会将方法变成单向操作。如设置false，则会删除标记列表中匹配的给定标记，且不会再度添加。如设置true，则将在标记列表中添加给定标记，并且不会再度删除。

### 返回值

返回`Boolean`值，给定标记存在于列表中返回true，标记不存在返回false

## replace()

将列表中已存在的token替换为一个新token。如果第一个参数token在列表中不存在，`replace()`立刻返回`false`，而不会将新token字符串添加到列表中。

### 语法

```js
tokenList.replace(oldToken, newToken);
```

### 参数

- oldToken：DOMString类型，想要替换的字符串。
- newToken：DOMString类型，表示要将oldToken字符串替换成的字符串。

### 返回值

boolean类型，如果oldToken被成功替换，返回true，否则返回false

## contains()

返回传入的参数是否在列表中，在则返回true，否则返回false。