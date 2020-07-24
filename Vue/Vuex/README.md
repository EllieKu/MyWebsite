# Vuex 
Vuex是專為Vue.js開發的**狀態管理模式**。採用集中式儲存管理所有組建的狀態，並以相應的規則保證狀態以一種可預測的方式變化。

![單向數據流概念](https://vuex.vuejs.org/vuex.png)

Vuex的應用核心是"Store"， 包含著應用中大部分的狀態(State)。和單純的全局對象有兩點差別：
1. Vuex 狀態儲存是響應式
2. 不能直接改變Store中的狀態， 唯一方法為**commit mutation**， 這樣可方便的追蹤每一個狀態的變化
----

## State
### `mapState`
`mapState`輔助函數幫助生成computed屬性：
```Javascript
// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```
或是字符串數組
```Javascript
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
```
或是使用展開語法(Spread syntax)
```Javascript
computed: {
  // 使用对象展开运算符将此对象混入到外部对象中
  ...mapState({
    // ...
  })
}
```
---
## Getter
從state中計算一些狀態。同computed屬性getter的返回值會根據它的依賴被緩存起來，只有當依賴值改變時才會重新計算。

接受`state`作為第一個參數，其他`getter`作為第二個參數