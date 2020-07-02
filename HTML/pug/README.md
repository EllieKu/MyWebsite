# pug

pug是一個對空白敏感的HTML模板編輯器,

## API
### Methods
    參數
    1. source: string, 需要編譯的pug模板
    2. options: 詳見options
    3. path: string, pug file的路徑
    4. callback: 回調函數用於接受渲染結果。同步執行。
    
 主要分成兩大類：
1. `pug.compile()`會把pug代碼編譯成JavaScript函數，並且可傳入一參數（局部變量`locals`),此時返回數據渲染的HTML字符串。此函數可重複使用，也可傳入不同數據。
    - `pug.compile(source, ?options)` -return: 包含局部變量渲染出的HTML函數
    - `pug.compileFile(path, ?options)` -return: 包含局部變量渲染出的HTML函數
    - `pug.compileClient(source, ?options)` -return: JS字符串
    - `pug.compileClientWithDependenciesTracked(source, ?options)` -return: 物件。與`compileClient`相似, 只有在需要實現監視"pug文件變動時"才使用該函數。
    - `pug.compileFileClient(path, ?options)` -return: JS字符串

2. `pug.render()`把編譯和渲染合併。故每次執行`render`時此模板函數就被重新編譯一遍，這在某程度上影響效能。可以配合使用options--`cache` 將編譯出的函數內部緩存。
    - `pug.render(source, ?options, ?callback)` -return: 渲染出的HTML字符串
    - `pug.renderFile(path, ?options, ?callback)` -return: 渲染出的HTML字符串

### Properties
-  `pug.filters` -自定義過濾器hash table。和options-- `filters`相同，但是為全局應用。與`options.filters`同時出現時filters options 優先選擇。
