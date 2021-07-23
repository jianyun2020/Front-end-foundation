- [location](#location)
  - [导航到一个新页面](#导航到一个新页面)
  - [强制从服务器加载当前页面](#强制从服务器加载当前页面)


# location

window.location 只读属性，返回一个 Location  对象，其中包含有关文档当前位置的信息。

尽管 window.location 是一个只读 Location 对象，你仍然可以赋给它一个 DOMString。这意味着您可以在大多数情况下处理 location，就像它是一个字符串一样：window.location = 'http://www.example.com'，是 window.location.href = 'http://www.example.com'的同义词 。

## 导航到一个新页面

只要赋给 location 对象一个新值，文档就会使用新的 URL 加载，就好像使用修改后的 URL 调用了  window.location.assign() 一样。需要注意的是，安全设置，如 CORS（跨域资源共享），可能会限制实际加载新页面。

```js
window.location.assign("http://www.example.com");

or

window.location = "http://www.example.com";


// 类似 HTTP 重定向到菜鸟教程
window.location.replace("https://www.runoob.com");

// 类似点击菜鸟教程的链接（a 标签）
window.location.href = "https://www.runoob.com";
```

## 强制从服务器加载当前页面

```js
window.location.reload(true);
```

