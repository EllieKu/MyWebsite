# Class and Style Bindings

## class: 綁定HTML class
- **Object syntax(對象)**: 傳給`v-bind:class`一個object, 動態切換class
    ```HTML
    <div
        class="static"
        v-bind:class="{ active: isActive, 'text-danger': hasError }">
    </div>
    ```
    或是object在`data`定義：
    ```HTML
    <div v-bind:class="classObject"></div> 
    ```
    ```JavaScript
    data: {
        classObject: {
            active: true,
            'text-danger': false
        }
    }
    ```
    或是`computed`返回的object值：
    ```HTML
    <div v-bind:class="classObject"></div>
    ```
    ```JavaScript
    data: {
        isActive: true,
        error: null
    },
    computed: {
        classObject: function () {
            return {
            active: this.isActive && !this.error,
            'text-danger': this.error && this.error.type === 'fatal'
            }
        }
    }
    ```
    </br>

- **Array Syntax(數組)**: 把array傳給`v-bind:class`, 獲取class列表
    ```HTML
    <div v-bind:class="[activeClass, errorClass]"></div>
    ```
    ```JavaScript
    data: {
        activeClass: 'active',
        errorClass: 'text-danger'
    }
    ```
    或是三元表達式(ternary expression)：
    ```HTML
    <div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
    ```
    或是在array中使用object:
    ```HTML
    <div v-bind:class="[{ active: isActive }, errorClass]"></div>
    ```
    </br>
- **With components(用在組件上)**: class在組件上使用時,會被渲染到該組件根元素上, 元素上已存在的class不會被覆蓋

## Inline Styles: 綁定行內樣式
- **Object syntax(對象)**: 傳給`v-bind:style`一個object. CSS property名用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名：
    ```HTML
    <div v-bind:style="{ color: 'red', fontSize: 30 + 'px' }"></div>
    ```
    或是綁定在`data`定義：
    ```HTML
    <div v-bind:style="styleObject"></div>
    ```
    ```JavaScript
    data: {
        styleObject: {
            color: 'red',
            fontSize: '13px'
        }
    }
    ```
    或是配合computed使用
    </br>
- **Array Syntax(數組)**:
    ```HTML
    <div v-bind:style="[baseStyles, overridingStyles]"></div>
    ```
- **Auto-prefixing(自動添加前綴)**: 當`v-bind:style`使用需要添加瀏覽器前綴的CSS property時, Vue.js會自動偵測並添加對應前綴
- **Multiple Values(多重值)**: 為`style`綁定的property提供一個包含多個值的array, 常用於提供多個帶前綴的值, 如下例只渲染被瀏覽器支持的值`display: flex`:
    ```HTML
    <div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
    ```
---
### 參考資料
[Class 与 Style 绑定](https://cn.vuejs.org/v2/guide/class-and-style.html)