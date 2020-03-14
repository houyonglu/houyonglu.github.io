---
title: 不常用 CSS 方法笔记
date: 2018-01-03 10:07:02
tags:
---

## 文字两端对齐

`text-align-last` 描述的是一段文本中最后一行在被强制换行之前的对齐规则，对于单行文本可实现两端对齐。

``` css
.text {
  text-align-last: justify;
}
```

## 设置鼠标事件

`pointer-events` 属性指定在什么情况下某个特定的图形元素可以成为鼠标事件的 `target`。主要用于 `svg`，对于普通元素，可用于取消鼠标事件。

``` css
.disabled {
  pointer-events: none;
}
```

## 文本模糊效果

设置模糊半径可控制模糊程度。

``` css
.blur {
  color: transparent;
  text-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
}
```

## 继承当前主体颜色

变量关键词 `currentColor` 可以让能够接受 `color` 值的属性继承当前主体颜色，多用于渐变和动画。

``` css
.tooltip {
  position: relative;
  color: #F44336;
  border: 2px solid currentColor;
}

.tooltip::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 0;
  transform: translate(-50%, 100%);
  border-style: solid;
  border-width: 10px 10px 0 10px;
  border-color: currentColor transparent transparent transparent;
}
```

## 黑白图像

CSS `filter` 属性可实现图像的模糊、锐化、变色效果，也可用于创建复杂的滤镜。

``` css
img.blackAndWhitePhoto {
  filter: grayscale(100%);
}
```

## content 属性 attr 实现解耦

``` html
<div data-tip="Some tips"></div>
```

``` css
div::after {
  content: attr(data-tip);
}
```
