# Template Syntax 模板語法

## 模板語法的表達方式
1. 插值
    - Mustach(雙大括號)：數據對象`data`的property值, 解釋為plain text
        ``` html 
        <span>Message: {{ msg }}</span>
        ```
    - HTML Tag: 使用`v-html`指令, 解釋為HTML
        ``` html
        <p>Using v-html directive: <span v-html="rawHtml"></span></p>
        ```
    - Attribute: 使用`v-bind`指令
        ``` html
        <button v-bind:disabled="isButtonDisabled">Button</button>
        ```
    - JavaScript表達式：
        ``` html
        {{ number + 1 }}
        {{ ok ? 'YES' : 'NO' }}
        {{ message.split('').reverse().join('') }}
        <div v-bind:id="'list-' + id"></div>
        ```
2. 指令
指令(directives)是帶有`v-`前綴的特殊attribute, 預期值是單個JavaScript表達式
    - 參數: 一些指令在 **：** 接受一個參數, 例如`v-bind`可以響應式更新HTML attribute
        ``` html
        <a v-bind:href="url">...</a>
        ```
    - 動態參數: **[** **]** 內會被作為JavaScript表達式進行動態求值, 其值作為指令的參數. 
        例如`data`的property attributeName其值為"href"，此绑定等同於 v-bind:href
        ``` html
        <a v-bind:[attributename]="url"> ... </a>
        ```
        - **對 動態参数值 的约束**
            預期值為String, 異常情況下值為null, null值可被顯性的用於移除綁定. 其他非String的類型會觸發警告
        - **對 動態参数表達式 的约束**
            1. 某些字符如空格和引號放在HTML attribute是無效的
            ``` html
            <!--觸發編譯警告-->
            <a v-bind:['foo' + bar]="value"> ... </a>
            ```
            2. 避免使用大寫來命名, 因HTML會全部強制轉為小寫
            ``` html
            <!--在 DOM 中使用模板時此代碼被轉為 `v-bind:[someattr]`。除非實例中有個名為“someattr”的 property，否則代碼不會工作。-->
            <a v-bind:[someAttr]="value"> ... </a>
            ```
3. 縮寫
    - v-bind **:**
    - v-on **@**
