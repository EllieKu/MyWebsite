# Vue.js
一些規則開發時建議遵守

---
## 優先級Ａ的規則: 必要的
- 組件名字應為多個單字: 避免名字衝突
- 在components中`data`值應為函數return的一個object
- `Props`定義應盡量詳細
- `v-for`設置`key`
- 避免`v-for`和`v-if`在同元素上使用: 下列解決方法：
	- 使用computed使其返回過濾後的列表
	- 將`v-if`移動至容器元素上(如`ul` . `ol`)
- 為組件style設置作用域: 此規則和*單文件組件*有關，下列解決方法：
	- `scoped`attribute
	- [CSS Modules](https://vue-loader-v14.vuejs.org/zh-cn/features/css-modules.html)
	- 基於class的類似[BEM](http://getbem.com/)的策略
- 私有property名:  用module scoping來維持外部不可訪問的私有性。如果無法做到，則用插件plugin、混入mixin 等不考慮作為公共API的自定義私有property使用 `$_`前綴命名，且加上named scope避免衝突

## 優先級B的規則：強烈推薦(增強可讀性)
- 單文件組件：只要有能拼接文件的建構系統，就把每個組件單獨分成文件
- 單文件組件文件名：
	- 單字大寫開頭(PascalCase) (較佳):  MyComponent.vue
	- 橫線連接 (kebab-case): my-component.vue
- 基礎組件名：也就是無邏輯、無狀態、展示類的組件應以一個特定的前綴命名
- 單例組件名：在 *每個頁面* 只使用一次，應以`The`前綴命名以示其唯一性( 代表組件不接受prop，如有表示此為可複用組件)
- 緊密耦合的組件名：與父組件緊密耦合的子組件應以父組件名作為前綴命名
- 組件命名的單詞順序：組件命名應以高級別(通常是一般化描述)單詞開頭、以描述性的修飾語結尾
- 自閉合標籤：在*單文件組件*、*字符串模板*和*JSX*中，沒有內容的組件標籤應為自閉合
- 模板中的組件名：
	- 在single-file components和string templates： PascalCase
	- 在DOM template：kebab-case
	- 在所有的地方都使用 kebab-case 同样是可以接受的
- JS/JSX的組件名：始終是PascalCase
- 完整單字的組件名：應使用完整單詞而不是縮寫
- Props名：
	- 命名：camelCase
	- 在templates或JSX：kebab-case
- 元素有多個attribute：應分多行撰寫,每個attribute一行
- template中應只包含簡單表達式,複雜的表達式應重構為computed或method
- 簡單的計算屬性：應把複雜的計算屬性分割為更簡單的property
	- 易於測試
	- 易於閱讀
	- 對需求變化更有適應性
- attribute 的值應帶有引號
- 指令縮寫應同時用或同時不用

## 優先級C的規則: 推薦(將選擇和認知成本最小化)
- components/instance的選項的順序： 應有統一的順序：
	1. 副作用 (触发组件外的影响)
		- `el`
	2. 全局感知 (要求组件以外的知识)
		- `name`
		- `parent`
	3. 组件类型 (更改组件的类型)
		- `functional`
	4. 模板修改器 (改变模板的编译方式)
		- `delimiters`
		- `comments`
	5. 模板依赖 (模板内使用的资源)
		- `components`
		- `directives`
		- `filters`
	6. 组合 (向选项里合并 property)
		- `extends`
		- `mixins`
	7. 接口 (组件的接口)
		- `inheritAttrs`
		- `model`
		- `props`/`propsData`
	8. 本地状态 (本地的响应式 property)
		- `data`
		- `computed`
	9. 事件 (通过响应式事件触发的回调)
		- `watch`
		- 生命周期钩子 (按照它们被调用的顺序)
			- beforeCreate
			- created
			- beforeMount
			- mounted
			- beforeUpdate
			- updated
			- activated
			- deactivated
			- beforeDestroy
			- destroyed
	10. 非响应式的 property (不依赖响应系统的实例 property)
		- `methods`
	11. 渲染 (组件输出的声明式描述)
		- `template`/`render`
		- `renderError`
- elements內attribute的順序： 應有統一的順序：
	1. 定义 (提供组件的选项)
		- `is`
	2. 列表渲染 (创建多个变化的相同元素)
		- `v-for`
	3. 条件渲染 (元素是否渲染/显示)
		- `v-if`
		- `v-else-if`
		- `v-else`
		- `v-show`
		- `v-cloak`
	4. 渲染方式 (改变元素的渲染方式)
		- `v-pre`
		- `v-once`
	5. 全局感知 (需要超越组件的知识)
		- `id`
	6. 唯一的 attribute (需要唯一值的 attribute)
		- `ref`
		- `key`
	7. 双向绑定 (把绑定和事件结合起来)
		- `v-model`
	8. 其它 attribute (所有普通的绑定或未绑定的 attribute)
	9. 事件 (组件事件监听器)
		- `v-on`
	10. 内容 (覆写元素的内容)
		- `v-html`
		- `v-text`
- components/instance如有多個properties,在之間空行可增加閱讀性
- 單文件組件應讓 `<script>`、`<template>` 和 `<style>`順序一致, `<style>`總是在最後

## 優先級D的規則:  謹慎使用(有潛在危險的模式)
- 在 `v-if`/`v-else-if`/`v-else` 中使用`key`：如果一组`v-if`+`v-else`的元素类型相同，最好使用`key` (because Vue is reusing the same element for render efficiency.)
- `scoped`中class選擇器比element選擇器更好
- 父子組件間通訊應優先透過prop和event,而不是`this.$parent`或變更prop
- Vuex 是 Vue 的官方類flux實現, 應優先透過Vuex管理全局狀態而不是通過`this.$root`
