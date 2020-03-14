---
title: JS 中的随机数
date: 2017-12-14 16:17:54
tags:
---

## 两数之间的随机数

``` js
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min
}
```

## 两数之间（包含两数）的随机整数

``` js
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min)
  max = Math.floor(max)
  return Math.floor(Math.random() * (max - min + 1)) + min
}
```

## 符合密码学要求的安全的随机值

``` js
window.crypto.getRandomValues(new Uint32Array(10))
```

## 简单的随机字符串

``` js
Math.random().toString(36).substr(2)
```

## 随机排列数组

使用 `Fisher–Yates shuffle` 算法可以高效地实现等概率的随机排序。

``` js
function shuffle(arr) {
  let index = arr.length

  while (index) {
    const random = Math.floor(Math.random() * index--)

    void ([arr[index], arr[random]] = [arr[random], arr[index]])
  }

  return arr
}
```

反例：

``` js
// Array.prototype.sort(comparefn) 并不能真正地随机打乱数组
// comparefn 对于同一组 a 、b 需要返回相同的比较结果
function shuffle(arr) {
  return arr.sort((a, b) => Math.random() - 0.5)
}
```
