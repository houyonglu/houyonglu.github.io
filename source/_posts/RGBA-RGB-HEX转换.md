---
title: 'RGBA, RGB, HEX 转换'
date: 2017-12-04 17:34:09
tags:
---

所有颜色均使用数组表示，如 `RGBA(0, 0, 0, 0.87)` 表示为 `[0, 0, 0, 0.87]` ，`RGB(33, 33, 33)` 表示为 `[33, 33, 33]`， `#212121` 表示为 `[21, 21, 21]`。

## RGBA to RGB

```js
function RGBAtoRGB(background, foreground) {
  const [backRed, backGreen, backBlue] = background
  const [foreRed, foreGreen, foreBlue, foreAlpha] = foreground

  return [
    Math.round((1 - foreAlpha) * backRed + foreAlpha * foreRed),
    Math.round((1 - foreAlpha) * backGreen + foreAlpha * foreGreen),
    Math.round((1 - foreAlpha) * backBlue + foreAlpha * foreBlue)
  ]
}

// RGBA(0, 0, 0, 0.87) => RGB(33, 33, 33)
RGBAtoRGB([255, 255, 255], [0, 0, 0, 0.87])
```

## RGB to HEX

```js
function RGBtoHEX([red, green, blue]) {
  return [red, green, blue].map(value => value.toString(16))
}

// RGB(33, 33, 33) => #212121
RGBtoHEX([33, 33, 33])
```

## HEX to RGB

```js
function HEXtoRGB([red, green, blue]) {
  return [red, green, blue].map(value => parseInt(value, 16))
}

// #212121 => RGB(33, 33, 33)
HEXtoRGB([21, 21, 21])
```
