---
title: React 高阶组件中的属性代理和反向继承
date: 2019-07-15 20:28:54
tags:
---

React 高阶组件（HOC）主要有两种类型：属性代理和反向继承。

## 属性代理（Props Proxy）

``` jsx
function propsProxyHOC(WrappedComponent) {
  return class EnhancedComponent extends React.Component {
    render() {
      return (
        <WrappedComponent {...this.props} />
      )
    }
  }
}
```

属性代理的作用：

* 操作 `props`。读取和操作传给 `WrappedComponent` 的 `props`。
* 通过 `Refs` 访问组件实例。读取或添加示例属性，调用实例方法。
* 提取组件状态。将 `WrappedComponent` 的状态提升到 `EnhancedComponent`。
* 用其他元素包裹 `WrappedComponent`。

## 反向继承（Inheritance Inversion）

``` jsx
function inheritanceInversionHOC(WrappedComponent) {
  return class EnhancedComponent extends WrappedComponent {
    render() {
      return super.render()
    }
  }
}
```

反向继承的作用：

* 提取组件 `state`。
* 通过 `super` 调用父类上的方法。
* 渲染劫持（Render Highjacking）。读取和操作组件中任何实例属性，条件渲染，包裹或修改输出的元素树。
