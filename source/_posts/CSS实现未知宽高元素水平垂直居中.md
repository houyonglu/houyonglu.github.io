---
title: CSS 实现未知宽高元素水平垂直居中
date: 2017-11-07 10:18:40
tags:
---

``` html
<div class="container">
  <span>Lorem ipsum</span>
</div>
```

## Absolute positioning + Transform

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

## Flexbox

``` css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## Grid

``` css
.container {
  display: grid;
}

span {
  margin: auto;
}
```
