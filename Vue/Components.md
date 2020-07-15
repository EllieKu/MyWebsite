# Component
- 組件是可複用的根實例, 所以和`new Vue`接收相同的Option,除了例外`el`
- 組件的複用: `data`必須是函式, 因此每個實例可以維護returned data object的獨立copy

## 註冊
- 全局註冊: 可用在根實例及組件樹內所有子組件模板中
	- `Vue.cpmponent`
- 局部註冊

## Prop
 在組件上註冊自定義 attribute, 當值傳給 prop attribute 時, 其變成該組件實例的property
```HTML
<blog-post
  v-for="post in posts"
  v-bind:key="post.id"
  v-bind:post="post"
></blog-post>
```
```JavaScript
Vue.component('blog-post', {
  props: ['post'],
  template: `
    <div class="blog-post">
      <h3>{{ post.title }}</h3>
      <div v-html="post.content"></div>
    </div>
  `
})
```
<br/>

## 監聽子組件事件
- 事件帶一個參數: 父組件透過`v-on`監聽子組件實例的事件, 子組件透過`$emit`傳入事件名稱來觸發; 
`$emit`可傳入第二個參數, 父組件`$event`來訪問值
	```HTML
	<button v-on:click="$emit('enlarge-text', 0.1)">
		Enlarge text
	</button>
	```
	```HTML
	<blog-post
	  v-on:enlarge-text="postFontSize += $event"
	></blog-post>
	```
- 組件上使用`v-model`: 
	- 将其 `value` attribute 绑定到名叫 `value` 的 prop 上
	- 在其 `input` 事件被触发时，将新的值通过自定义的 `input` 事件抛出
	```JavaScript
	Vue.component('custom-input', {
	  props: ['value'],
	  template: `
		<input
		  v-bind:value="value"
		  v-on:input="$emit('input', $event.target.value)"
	 	>
	  `
	})
	```
	```HTML
	<custom-input v-model="searchText"></custom-input>
	```
<br/>

## slot插槽
<br/>

## 動態組件
在不同組件中切換, 透過`<component>`標籤加上 `is` attribute實現
```HTML
<component v-bind:is="currentTabComponent"></component>
```

---
### 參考資料
[組件基礎](https://cn.vuejs.org/v2/guide/components.html)