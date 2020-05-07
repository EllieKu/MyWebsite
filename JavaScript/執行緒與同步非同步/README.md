# Web瀏覽器中的JavaScript
**Window物件** 代表web瀏覽器的一個視窗(window)或是頁框(frame)
- 位於scope chain的最頂端,它的特性有個名為window的特性永遠指向它自己.
- document 為其特性之一: 指向一個Document物件,代表顯示於視窗中的內容 
 
## 在HTML內嵌script的方法
1. inline - 介於`<script></script>`之間
2. 用`<script scr="">`引入外部檔案
3. 置於EventHandler屬性中
4. javascript:URL -URL的主體為任意的JS字串,要由JS直譯器執行
   
## JavaScript程式的執行 -單執行緒()
第一階段- document載入,程式依出現順序執行,從script來的程式被執行;一旦所有script執行完畢進入第二階段
第二階段- 非同步(asynchronous)、事件驅動(event-driven)
 -`load`事件為事件驅動最早發生的事件之一,表示文件已被完整載入可供操作
 -`<script defer>`script會暫緩,等document載入與解析完後才執行
 -`<script async>`script載入完成會先執行,document會暫緩解析

 ## JavaScript程式的執行(詳細)
 1. Web創建Document物件並開始解析.將Element物件與nodes加入文件 (document.readyState = "loading")
 2. 若遇到沒有defer或async的script,將此腳本加入document並同步執行(腳本在下載與執行時doc暫停解析)
 3. 若遇到async的腳本會下載(doc繼續解析),一旦腳本載好立刻執行(doc暫停解析)
 4. 當doc解析完畢時(document.readtState = "interactive")
 5. defer的腳本依doc出現順序執行
 6. 觸發DOMContnteLoaded事件,執行階段從同步轉為非同步的事件驅動
 7. doc已被完全解析,且async腳本已載入執行完,window物件觸發load事件(document.readyState = "complete")
 8. 事件處理器開始運作回應
 
---
### 參考文章
1. David Flanagan.(黃銘偉譯) 2012. Javascript大全. 307-339. 台北市. 碁峯資訊.
2. https://ithelp.ithome.com.tw/articles/10200054
