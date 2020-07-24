# Vuex 
Vuex是專為Vue.js開發的**狀態管理模式**。採用集中式儲存管理所有組建的狀態，並以相應的規則保證狀態以一種可預測的方式變化。

![單向數據流概念](https://vuex.vuejs.org/vuex.png)

Vuex的應用核心是"Store"， 包含著應用中大部分的狀態(State)。和單純的全局對象有兩點差別：
1. Vuex 狀態儲存是響應式
2. 不能直接改變Store中的狀態， 唯一方法為**commit mutation**， 這樣可方便的追蹤每一個狀態的變化
----

## State
Vuex使用**single state tree**，指一個對象包含了全部應用層級的狀態，作為一個“唯一數據源“的存在
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
或是字符串array
```Javascript
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
```
或是使用object展開語法(Spread syntax)
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
```Javascript
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```
----
## Mutation
- 更改store中state的唯一方法
- 每個mutation都有一個字符串的事件類型(type)和一個回調函數(handler)，以相應的type調用`store.commit`觸發mutation handler

- 接受`state`作為第一個參數，`payload`作為第二個參數傳參
```JavaScript
store.commit('increment', {
amount: 10
})
```
```JavaScript
mutations: {
increment (state, payload) {
    state.count += payload.amount
}
}
```
或是直接包含type屬性的object提交mutation，將整個object作為payload
```JavaScript
store.commit({
  type: 'increment',
  amount: 10
})
```
```JavaScript
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```
### 注意事項
1. 最好提前在store初始化完所有所需屬性
2. 當需要在object添加新屬性時，應該：
    - 使用`Vue.set(obj, 'newProp', 123)`
    - 或是以new object替換ole object 
  `state.obj = { ...state.obj, newProp: 123 }`
3. 可以使用常量替代mutation事件類型，[詳見](https://vuex.vuejs.org/zh/guide/mutations.html)
4. 必須是**同步函數**
----

## Action
- 可以提交的是mutation
- 可以**異步操作**
- 接受一個與store實例具有相同方法和屬性的context對象，調用`context.commit`提交mutation，或是`context.state`和`context.getters`獲取state和getters
- `store.dispatch`可以處理觸發的action的處理函數返回的Promise，且仍舊返回Promise 
```Javascript
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
```
```Javascript
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```
- 可以利用`async/await`

----
## Module
每個module擁有自己的state、mutation、action、getter
```Javascript
const moduleA = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```
- 模塊內的mutation和getter，接收的第一個參數為**局部**`state`
- 模塊內的action，接收`context`