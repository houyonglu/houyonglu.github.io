---
title: CSS 百分比值的理解和应用
date: 2017-11-07 11:41:13
tags:
---

## 百分比值是相对值
在大多数情况下，即使将一个属性的 [指定值](https://developer.mozilla.org/zh-CN/docs/Web/CSS/specified_value) 设置为相对值，其 [应用值](https://developer.mozilla.org/zh-CN/docs/Web/CSS/used_value) 也会被替换为像素值。也就是说， **百分比值的属性的最终值为像素值，并由它的参照物决定**。


## 百分比值的参照

#### width & Height
`margin` 和 `padding` 参照都是包含块的宽度。当一个元素的高度使用百分比值，如果其包含块没有明确的高度定义，且这个元素不是绝对定位，则该百分比值等同于 `auto`。如果元素是根元素，它的包含块是视口提供的初始包含块，初始包含块任何时候都被认为是有高度定义的，且等于视口高度。

#### margin & padding
对于某个元素的 `margin` 和 `padding`，其任意方向的百分比值的参照包含块的宽度。如果包含块的宽度取决于该元素，那么百分比值的使用结果相当于未定义。

#### top & right & bottom & left
`top` `bottom` 参照包含块的高度，`bottom` `left` 参照包含块的宽度。

#### background-position
`background-position` 参照一个减法计算值，计算公式如下：

``` js
positionX = (containerWidth - backgroundImageWidth) * percentX;
positionY = (containerHeight - backgroundImageHeight) * percentY;
```

#### font-size
参照直接父元素的 `font-size`

#### line-height
参照元素自身的`font-size`

#### vertical-align
参照元素自身的`line-height`

#### border-radius
`border-radius` 水平半轴参照盒模型的宽度，垂直半轴参照盒模型的高度。

#### transform
`translateX` `scaleX` 参照变换边缘的宽度， `translateY` `scaleY`参照变换边缘的高度。

## 百分比值的继承
当百分比值用于可继承属性时，只有最终值会被继承，而不是百分比值本身。

## 百分比值的应用

#### 等比缩放

``` html
<div class="container">
  <div class="box"></div>
</div>
```

``` css
.container {
  position: relative;
  height: 0;
  padding-bottom: 50%;
}

.box {
  position: absolute;
  width: 100%;
  height: 100%;
}
```

#### 未知宽高元素水平垂直居中

``` html
<div class="container">
  <span>Lorem ipsum</span>
</div>
```

``` css
.container {
  position: relative;
}

span {
  display: inline-block;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
```
