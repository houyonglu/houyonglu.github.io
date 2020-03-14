---
title: CSS 新特性中的层叠上下文及影响
date: 2018-01-26 17:08:21
tags:
---

## CSS中层叠上下文

形成条件：

* 根元素 （`HTML`）
* `z-index` 值不为 `auto` 的绝对/相对定位
* 一个 `z-index` 值不为 `auto` 的 `Flex` 项目（`flex item`）
* `position: fixed`
* `opacity` 属性值小于 `1`
* `transform` 属性值不为 `none`
* `mix-blend-mode`性值不为 `normal`
* `filter` 值不为 `none`
* `will-change` 中指定了任意 CSS 属性
* `mix-blend-mode` 属性值不为 `normal`
* `-webkit-overflow-scrolling` 属性被设置 `touch`

总结：

* 给一个 HTML 元素定位和 `z-index` 赋值创建一个层叠上下文。
* 层叠上下文可以包含在其他层叠上下文中，并且一起创建一个有层级的层叠上下文。
* 每个层叠上下文完全独立于它的兄弟元素：当处理层叠时只考虑子元素。
* 每个层叠上下文是自包含的：当元素的内容发生层叠后，整个该元素将会在父层叠上下文中按顺序进行层叠。

内容来自: [层叠上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)

## 对普通元素的影响

* 提升元素的层叠顺序
* 限制 `position: fixed` 的跟随效果
* 改变 `overflow` 对 `absolute` 元素的限制
* 限制 `absolute` 元素的 `100%` 宽度大小
* 进行变换时造成变换元素的父元素闪烁

[Check which CSS3 features the browser recognizes](https://codepen.io/anon/pen/ZvgOLO) 是我制作的一个简单 Demo，用于展示 CSS 新特性是如何提升元素的层叠顺序的。

## 解决方案

``` html
<div class="parent">
  <div class="transform"></div>
  <div class="sibling"></div>
</div>
```

``` css
/* 显式设置父元素的层叠顺序 */
.parent {
  position: relative;
  z-index: 1;
}

/* 显式设置变换元素的层叠顺序 */
.transform {
  position: relative;
  z-index: -1;
}

/* 显式设置变换元素的兄弟元素的层叠顺序 */
.sibling {
  position: relative;
  z-index: 1;
}
```
