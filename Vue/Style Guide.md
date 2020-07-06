# Vue.js
一些規則開發時建議遵守

---
## 優先級Ａ的規則: 必要的
- 組件名字應為多個單字: 避免名字衝突
- 組建數據:  在組件components中`data`值應為函數return的一個object
- `Props`定義:  應盡量詳細
- `v-for`設置`key`
- 避免`v-for`和`v-if`在同元素上使用: 下列解決方法：
	- 使用計算屬性，使其返回過濾後的列表
	- 將`v-if`移動至容器元素上(如`ul` . `ol`)
- 為組件style設置作用域: 此規則和*單文件組件*有關，下列解決方法：
	- `scoped`attribute
	- [CSS Modules](https://vue-loader-v14.vuejs.org/zh-cn/features/css-modules.html)
	- 基於class的類似[BEM](http://getbem.com/)的策略
- 私有property名:  用module scoping來維持外部不可訪問的私有性。如果無法做到，則用插件plugin、混入mixin 等不考慮作為公共API的自定義私有property使用 `$_`前綴命名，且加上named scope避免衝突

## 優先級B的規則：強烈推薦(增強可讀性)
- 單文件組件：只要有能拼接文件的建構系統，就把每個組件單獨分成文件
- 單文件組件名字：
	- 單字大寫開頭(PascalCase) (較佳):  MyComponent.vue
	- 橫線連接 (kebab-case): my-component.vue
- 基礎組件名：也就是無邏輯、無狀態、展示類的組件應以一個特定的前綴命名
- 單例組件名：在*每個頁面*只使用一次，應以`The`前綴命名以示其唯一性( 代表組件不接受prop，如有表示此為可複用組件)
- 緊密耦合的組件名：與父組件緊密耦合的子組件應以父組件名作為前綴命名
- 組件命名的單詞順序：組件命名應以高級別(通常是一般化描述)單詞開頭、以描述性的修飾語結尾
- 自閉合標籤：在*單文件組件*、*字符串模板*和*JSX*中，沒有內容的組件標籤應為自閉合

### 待續
