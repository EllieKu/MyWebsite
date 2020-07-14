# Vue Router

## 基礎
+ 使用`<router-link>`傳入 to 屬性導航連結位置,`<router-link>`默認會被渲染成`<a>`
+ 使用`<router-view>`渲染

```HTML
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <router-view></router-view>
</div>
```
```JavaScript
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

const router = new VueRouter({
  routes
})

const app = new Vue({
  router
}).$mount('#app')

```
## 動態路由匹配
使用"動態路徑參數"匹配到
