# Computed / Watch

## Computed

- 基於響應式依賴結果會被**緩存**, 只有在依賴的響應式property發生改變才會重新求值 (如果非響應式property,則計算屬性不會更新)
- 注意: 如果在computed使用箭頭函數，則`this`不會指向此組件實例，不過仍可以將其實例作為函数的第一个参数來訪問
    ```javascript
    computed: {
        aDouble: vm => vm.a * 2
    }
    ```
- 默認只有 getter ,不過也可以定義 setter; 如下在運行 `vm.fullName = 'John Doe'` 時，setter 會被调用，`vm.firstName` 和 `vm.lastName` 也會被更新。
    ```javascript
    computed: {
        fullName: {
            // getter
            get: function () {
                return this.firstName + ' ' + this.lastName
            },
            // setter
            set: function (newValue) {
                var names = newValue.split(' ')
                this.firstName = names[0]
                this.lastName = names[names.length - 1]
            }
        }
    }
    ```
## Watch
- 當數據變化時需要執行異步或開銷較大的的操作時
- Vue instance 會在實例化時調用`$watch()`, 遍歷watch對象的每一個property
    ```javascript
    var vm = new Vue({
        data: {
            a: 1,
            b: 2,
            c: 3,
            d: 4,
            e: {
                f: {
                    g: 5
                }
            }
        },
        watch: {
            a: function (val, oldVal) {
            console.log('new: %s, old: %s', val, oldVal)
            },
            b: 'someMethod', // 方法名
            c: {   // 该回调会在任何被侦听的对象的 property 改变时被调用，不论其被嵌套多深
                handler: function (val, oldVal) { /* ... */ },
                deep: true
            },
            d: {  // 该回调将会在侦听开始之后被立即调用
                handler: 'someMethod',
                immediate: true
            },
            e: [ 'handle1', // 你可以传入回调数组，它们会被逐一调用
                function handle2 (val, oldVal) { /* ... */ },
                {
                    handler: function handle3 (val, oldVal) { /* ... */ },
                    /* ... */
                }
            ],
            // watch vm.e.f's value: {g: 5}
            'e.f': function (val, oldVal) { /* ... */ }
        }
    })
    vm.a = 2 // => new: 2, old: 1
    ```
- 注意: 不應使用箭頭函數來定義watcher函數, 因箭頭函數綁定了不及作用域的上下文, `this`不會指向Vue實例
---
### 參考資料
[计算属性和侦听器](https://cn.vuejs.org/v2/guide/computed.html)