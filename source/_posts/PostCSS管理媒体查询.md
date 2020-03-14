---
title: PostCSS 管理媒体查询
date: 2018-01-06 16:34:46
tags:
---

## 断点设置

``` css
:root {
  /* 容器的水平间距，作为断点的偏移量 */
  --gap: 32px;

  /* 960, 1152, and 1344 可以被 12 和 16 整除 */
  --tablet: 769px;

  /* 960px container + 4rem */
  --desktop: calc(960px + var(--gap) * 2);

  /* 1152px container + 4rem */
  --widescreen: calc(1152px + var(--gap) * 2);

  /* 1344px container + 4rem */
  --fullhd: calc(1344px + var(--gap) * 2);
}
```

查阅 [Bulma Responsiveness](https://bulma.io/documentation/overview/responsiveness/)。

## 自定义媒体查询

按当前 [CSS Media Queries Level 4](https://drafts.csswg.org/mediaqueries/#mq-range-context) 规范，不能在媒体查询中使用 `var()`，因为媒体查询不从 `:root` 继承。

``` css
@custom-media --mobile (width < 769px);

@custom-media --tablet-only (769px <= width < 1024px);

@custom-media --touch (width <= 1024px);

@custom-media --tablet (width >= 769px);

@custom-media --desktop-only (1024px <= width < 1216px);

@custom-media --desktop (width >= 1024px);

@custom-media --widescreen-only (1216px <= width < 1408px);

@custom-media --widescreen (width >= 1024px);

@custom-media --fullhd (width >= 1408px);
```

## 使用媒体查询

``` css
@media (--mobile) and (orientation: landscape) {
  /* styles */
}
```
