---
title: FastRoute 的 JS 最小实现
date: 2018-10-12 18:30:39
tags:
---

[nikic/fast-route](https://github.com/nikic/FastRoute) 是 PHP 中的快速路由类，通过将多条路由正则表达式合并为一条后进行匹配以提高性能。

``` js
class Router {
  constructor(routes) {
    this.routeMap = []

    let offset = 1
    const regexRoutes = Object.entries(routes).map(([ route, handler ]) => {
      const paramNames = []
      const regexRoute = route.replace(/:(\w*)/g, (_, paramName) => {
        paramNames.push(paramName)
        return '([^/]+)'
      })

      this.routeMap[offset] = { handler, paramNames }

      if (paramNames.length > 0) {
        offset += paramNames.length
        return regexRoute
      }

      offset += 1
      return `(${regexRoute})`
    })

    this.regex = new RegExp(`^(?:${regexRoutes.join('|')})$`)
  }

  dispatch(path) {
    const matches = path.match(this.regex)

    // 404
    if (!matches) return undefined

    let offset = matches.findIndex((match, index) => (index > 0) && !!match)
    const { handler, paramNames } = this.routeMap[offset]
    const routeParams = Object.fromEntries(
      paramNames.map(paramName => [paramName, matches[offset++]])
    )

    handler(routeParams)
  }
}
```

使用：

``` js
const r = new Router({
  '/owner': () => console.log('owner'),
  '/:owner': params => console.log(params),
  '/:owner/:repo': params => console.log(params),
  '/:owner/:repo/branches/:branch': params => console.log(params),
})

// => owner
r.dispatch('/owner')

// => { owner: 'facebook' }
r.dispatch('/facebook')

// => { owner: 'facebook', repo: 'react' }
r.dispatch('/facebook/react')

// => { owner: 'facebook', repo: 'react', branch: 'facts' }
r.dispatch('/facebook/react/branches/facts')

// => 
r.dispatch('/facebook/react/branches/facts/page/2')
```
