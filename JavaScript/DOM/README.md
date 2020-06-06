# DOM

## 寫入方法
1. Node.textContent
表示了節點或其後代的文字內容。
- 如設置此方法會替換其所有子節點留下此節點和值
- 能獲取所有元素包含`<script>`和`<style>` (innerText不能)
- 會回傳hidden element

2. HTMLElement.innerText
表示了**已渲染**節點及其後代,IE創造
- 如設置此方法替換並**永久摧毀**其所有子節點 (不能再插入element)
- 能表現style故能觸發reflow
- 不回傳hidden element

3. Element.innerHTML