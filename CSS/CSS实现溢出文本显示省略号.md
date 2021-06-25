# 单行文本

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
  display: -webkit-box; // 将对象作为弹性伸缩盒子模型显示
  -webkit-line-clamp: 2; // 将块容器中的内容限制为指定的行数.
  -webkit-box-orient: vertical; // 设置或检索伸缩盒对象的子元素的排列方式
}
```

## 通过绝对定位实现

