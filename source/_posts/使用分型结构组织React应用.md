---
title: 使用分型结构组织 React 应用
date: 2019-11-16 20:58:17
tags:
---

> 分形（fractal），又称碎形、残形，通常被定义为“一个粗糙或零碎的几何形状，可以分成数个部分，且每一部分都（至少近似地）是整体缩小后的形状”，即具有自相似的性质。分形在数学中是一种抽象的物体，用于描述自然界中存在的事物。人工分形通常在放大后能展现出相似的形状。分形也被称为扩展对称或展开对称。如果在每次放大后，形状的重复是完全相同的，这被称为自相似。分形在不同的缩放级别上可以是近似相似的。

## 目录结构

``` text
src/
  assets/
    logo.svg
  components/
    Footer/
      index.tsx
  scenes/
    Main/
      Home/
        components/
          Carousel/
            assets/
              banner-1.png
              banner-2.png
            index.tsx
          List/
            components/
              ListItem/
                index.tsx
            index.tsx
        index.tsx
      My/
        index.ts
    Account
      SignUp/
        index.tsx
      SignIn/
        index.tsx
      PasswordReset/
        index.tsx
  index.tsx
```
