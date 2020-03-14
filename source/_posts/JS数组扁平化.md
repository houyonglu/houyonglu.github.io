---
title: JS 数组扁平化
date: 2018-04-12 15:01:11
tags:
---

## 扁平一层

``` js
function flatten(arr) {
  return Array.prototype.concat.apply([], arr)
}

// => [1, 2, 3, [4, 5, [6, 7, [8, 9, [10, 11]]]], 12, 13]
flatten([1, [2, 3, [4, 5, [6, 7, [8, 9, [10, 11]]]]], [12, 13]])
```

## 扁平所有层

``` js
function flatten(arr) {
  return arr.reduce((prev, curr) => {
    return Array.isArray(curr)
      ? prev.concat(flatten(curr))
      : prev.concat([curr])
  }, [])
}

// => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
flatten([1, [2, 3, [4, 5, [6, 7, [8, 9, [10, 11]]]]], [12, 13]])
```

## 扁平 N 层

``` js
function flatten(arr, depth) {
  return arr.reduce((prev, curr) => {
    return Array.isArray(curr)
      ? prev.concat(depth > 1 ? flatten(curr, depth - 1) : curr)
      : prev.concat([curr])
  }, [])
}

// => [1, 2, 3, 4, 5, 6, 7, [8, 9, [10, 11]], 12, 13]
flatten([1, [2, 3, [4, 5, [6, 7, [8, 9, [10, 11]]]]], [12, 13]], 3)
```
