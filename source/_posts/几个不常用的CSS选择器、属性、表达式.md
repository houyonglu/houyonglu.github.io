---
title: 几个不常用的 CSS 选择器、属性、表达式
date: 2017-11-13 14:10:48
tags:
---

## 部分CSS选择器、属性、表达式

### attr

> `attr()` 表达式用来获取选择到的元素的某一 HTML 属性值，并用于其样式。它也可以用于伪元素，属性值采用伪元素所依附的元素。

### content
>`content` 属性用于在元素的  ::before 和 ::after 伪元素中插入内容。使用 `content` 属性插入的内容都是匿名的可替换元素。

### :empty
> `:empty` 表示没有子元素的元素。子元素只可以是元素节点或文本（包括空格），无论一个元素是否为 (empty 或 not), 注释或处理指令都不会产生影响。

### :valid & :invalid
> `:valid` 和 `:invalid` 表示任何其内容根据设置的输入类型正确（不正确）地验证的 `<input>` 或  `<input>` 元素。

### :target
> 伪类选择器 `:target` 代表一个特殊的元素，它的id是URI的片段标识符。

### ::selection
> `::selection` 应用于文档中被用户高亮的部分（比如使用鼠标或其他选择设备选中的部分）。

## 一些应用

### Tooltip

``` html
<button data-tip="some tips">Click me</button>
```

``` css
button {
  margin-top: 50px;
  position: relative;
}

button::after {
  content: attr(data-tip);
  display: none;
  position: absolute;
  width: 100%;
  height: 30px;
  line-height: 30px;
  top: -40px;
  left: 0;
  color: #FFF;
  border-radius: 2px;
  background-color: rgba(0, 0, 0, .8);
}

button:hover::after {
  display: block;
}
```

### 为只有 href 属性的的链接添加文本值

``` css
a[href^='http']:empty::before {
  content: attr(href);
}
```
