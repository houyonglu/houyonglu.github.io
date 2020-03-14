---
title: PAC 实现基于域名的自动代理
date: 2017-11-23 18:50:48
tags:
---

## 最简单的 PAC 示例

``` js
function FindProxyForURL(URL, HOST) {
  // google.com 则通过本地 8686 端口 SOCKS5 协议访问
  // 其它域名直接访问
  return HOST === 'google.com' ? 'SOCKS5 127.0.0.1:8686' : 'DIRECT'
}
```

## 适用于 shadowSocks 轻量高效的配置文件

<small>*注： 以下将 `com.hk` 、 `co.jp` 、 `gov.cn` 等视为顶级域名（TLD）。*</small>

``` js
// 黑名单
const blacklist = {
  'google.com.hk': 1,
  // ...
}

function FindProxyForURL(URL, HOST) {
  // 分割域名并反转
  // www.google.com.hk  =>  ['hk', 'com', 'google', 'www']
  const splitHost = HOST.split('.').reverse()

  // 获取二级域名的偏移值
  const offset = ['com', 'co', 'org', 'net', 'gov'].includes(splitHost[1]) ? 3 : 2

  // 取出二级域名
  // ['hk', 'com', 'google', 'www']  =>  google.com.hk
  const SLD = splitHost.slice(0, offset).reverse().join('.')

  // 如果黑名单中存在该二级域名则通过 shadowSocks 访问
  return Object.hasOwnProperty.call(blacklist, SLD)
    ? 'SOCKS5 127.0.0.1:8686'
    : 'DIRECT'
}
```

## 将域名绑定到本地 Web 服务器
``` js
function FindProxyForURL(URL, HOST) {
  return HOST === 'laravel.dev' ? 'HTTP 127.0.0.1:80' : 'DIRECT'    
}
```
<small>*注： 该方法同样适用于拦截指定域名。*</small>

## 其它高级用法
PAC 还支持很多其它的高级用法，具体见 [PAC Functions](https://findproxyforurl.com/pac-functions/)
