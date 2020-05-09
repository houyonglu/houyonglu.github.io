---
title: CSS 实现 1px 边框
date: 2018-10-12 18:17:50
tags:
---

``` scss
.border-1px {
  position: relative;

  &::before {
    position: absolute;
    left: 0;
    top: 0;
    display: block;
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    border: 1px solid #000;
    pointer-events: none;
    content: '';

    @media (min-device-pixel-ratio: 2) {
      width: 200%;
      height: 200%;
      transform: scale(.5);
    }

    @media (min-device-pixel-ratio: 3) {
      width: 300%;
      height: 300%;
      transform: scale(.33);
    }
  }
}
```
