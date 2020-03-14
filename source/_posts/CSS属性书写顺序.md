---
title: CSS 属性书写顺序
date: 2019-04-23 19:10:54
tags:
---

## Grouped by Type

* Display & Flow
* Positioning
* Dimensions
* Margins, Padding, Borders, Outline
* Typographic Styles
* Backgrounds
* Opacity, Cursors, Generated Content

## Demo

``` scss
.some {
  // Display & Flow
  display: flex;
  visibility: hidden;
  float: left;
  clear: both;

  // Positioning
  z-index: auto;
  position: relative;
  top: 0;
  right: 0;

  // Dimensions
  width: 100%;
  height: 100px;
  overflow: hidden;

  // Margins, Padding, Borders, Outline
  margin: 0 auto;
  padding: 10px;
  border: 1px solid #000000;
  outline: none;
  list-style: square inside;
  border-collapse: inherit;

  // Typographic Styles
  font: 1.2em "Fira Sans", sans-serif;
  text-align: center;
  white-space: nowrap;
  color: #000000;

  // Backgrounds
  background: content-box radial-gradient(crimson, skyblue);
  box-shadow: 10px 5px 5px red;
  mask: url(masks.svg#star) 40px 20px;

  // Opacity, Cursors, Generated Content
  opacity: 0;
  cursor: pointer;
  content: '';
  quotes: '"' '"' "'" "'";
}
```
