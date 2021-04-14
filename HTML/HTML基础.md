# 空元素(Empty elements / void elements)

不包含任何内容的元素称为**空元素**。比如`<img>`标签。

# 布尔属性

有时你会看到没有值的属性，这些属性被称为**布尔属性**，它们只能有跟它的属性名一样的属性值。例如`disabled`属性

```html
<input type="text" disabled="disabled">
或者
<input type="text" disabled >
```

# 实体引用： 在HTML中包含特殊字符

在HTML中，字符 `<`, `>`, `"`, `'` 和 `&` 是特殊字符. 它们是HTML语法自身的一部分, 使用**字符引用**将这些字符包含进你的文本中。

|原义字符|等价字符引用|
|-|-|
|`<`|`&lt;`|
|`>`|`&gt;`|
|`"`|`&quot;`|
|`'`|`&apos;`|
|`&`|`&amp;`|

# HTML的头部元素

`<head>`元素的作用是保存页面的一些**元素据**。

## 元素据

**Metadata——元素据**，简单来说就是描述数据的数据。例如，一个HTML文件是一种数据，但HTML文件也能在`<head>`元素中包含描述该文档的元数据，比如该文件的作者和概要。

# 超链接

通过`<a>`元素来创建基本的链接

**下载链接**时使用`download`属性：

```html
<a href="https://download.mozilla.org/?product=firefox-latest-ssl&os=win64&lang=zh-CN" download="firefox-latest-64bit-installer.exe">
下载最新的 Firefox 中文版 - Windows（64位）
</a>
```

**电子邮件链接**

```html
<a href="mailto:nowhere@mozilla.org">向 nowhere 发邮件</a>
```

## 尽可能使用相对链接

- 首先，检查代码要容易得多——相对URL通常比绝对URL短得多，这使得阅读代码更容易。
- 其次，在可能的情况下使用相对URL更有效。当使用绝对URL时，浏览器首先通过DNS查找服务器的真实位置，然后再转到该服务器并查找所请求的文件。另一方面，相对URL，浏览器只在同一服务器上查找被请求的文件。因此，如果你使用绝对URL而不是相对URL，你就会不断地让你的浏览器做额外的工作，这意味着它的效率会降低。