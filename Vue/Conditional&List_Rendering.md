# Conditional&List Rendering 條件渲染

## `v-if`
- DOM操作, 只在指令的表達式返回truthy值時被渲染
- 惰性的, 只有在條件為真時才渲染
- 切換時, element 和它的directives / components 被銷毀並重建
- 使用`<template`分組, 最終選染將不包含`<template>`元素
    ```HTML
    <template v-if="ok">
        <h1>Title</h1>
        <p>Paragraph</p>
    </template>
    ```
- 可搭配`v-else`, 必須緊跟在`v-if`或`v-else-if`後, 否則不被識別
    ```HTML
    <h1 v-if="awesome">Vue is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>
    ```
- `v-else-if`可連續使用
    ```HTML
    <div v-if="type === 'A'">A</div>
    <div v-else-if="type === 'B'">B</div>
    <div v-else-if="type === 'C'">C</div>
    <div v-else>Not A/B/C</div>
    ```
- `key`管理: vue為高效的渲染元素, 若模板元素相同則複用不會重新渲染; 使用`key` attribute表示此元素完全獨立不要複用
- 避免同時使用`v-if`和`v-for`: 查看[風格指南](https://cn.vuejs.org/v2/style-guide/#%E9%81%BF%E5%85%8D-v-if-%E5%92%8C-v-for-%E7%94%A8%E5%9C%A8%E4%B8%80%E8%B5%B7%E5%BF%85%E8%A6%81), 當一起使用時`v-for`比`v-if`具有更高的優先級. 詳見[列表渲染教程](https://cn.vuejs.org/v2/guide/list.html#v-for-object)
</br>

## `v-show`
- CSS操作, 切換元素的`display`
- 始終被渲染並保留在DOM中. 
</br>

## `v-for`
- 使用特殊語法 `v-for = 'item in items'`
    - 若對應值為 **Array** :
        - 支持第二個參數-索引: `v-for = '(item, index) in items'`
        - 可用`of`代替`in`做分隔符: `v-for = 'item of items'`
    - 若對應值為 **Object** :
        - 支持第二個參數-鍵(key): `v-for = '(value, key) in items'`
        - 支持第三個參數-索引: `v-for = '(value, key, index) in items'`
- **[key](https://cn.vuejs.org/v2/api/#key)** : 若數據項順序(order of the data items)改變, Vue 不會移動 DOM 元素來匹配數據項順序, 而是就地更新每個元素. 此默認模式適用於**不依賴子組件狀態**或**臨時 DOM 狀態(e.g. form input values)的列表渲染輸出**. `key`提供 Vue 識別每個節點, 進而重用和重新排列現有元素
- 數組變更方法: Vue 將 array 的方法進行了包裹, 故會觸發視圖更新:
    - `push()`
    - `pop()`
    - `shift()`
    - `unshift()`
    - `splice()`    
    - `sort()`
    - `reverse()`
- 數組替換: 不會變更原始array, 返回一個新數組
    - `filter()`
    - `concat()`
    - `slice()`
- 顯示過濾/排序後的結果: 可使用`computed`或`methods`來返回
- 用`<template>`渲染一段包含多個元素的內容


---
### 參考資料
[条件渲染](https://cn.vuejs.org/v2/guide/conditional.html)
[列表渲染](https://cn.vuejs.org/v2/guide/list.html)