# Vue Router

+ 使用`<router-link>`傳入to屬性導航連結位置,`<router-link>`默認會被渲染成`<a>`
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