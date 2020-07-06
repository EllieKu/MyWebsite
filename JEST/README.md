# JEST 
**開發準備**:  一款JavaScript測試工具
**立即回饋**: 快速, 在執行期間監視文件的變化
**快照測試**: 捕捉大型物件快照簡化測試, 並分析如何隨時間變化

------
## Matchers (匹配器)	[待研究]
JEST以"matchers"去使用不同方式測試值(value), 詳細見[expect API](https://jestjs.io/docs/en/expect)
1. `expect`系列: 期望對象
	- `expect(value)` :  每次測試一個值時都會用到expect函數, 通常伴隨“matchers"函數來assert值
	- `expect.extend(matchers)`:  將自定義matchers函數添加到JEST
	[待研究]
	- `expect.anything()`:  匹配除`null`和`undefined`的所有
	- `expect.any(constructor)`: 匹配被given constructor創造的所有
	- 
2. `.not`: 所有匹配器都可使用取相反
3. `.resolves`/`.rejects`: 對於 *Promise* 函數可使用
3. `toBe`系列: 確認想判斷什麼條件
	- `toBe(value)`:  呼叫 *Object.is* 判斷值否嚴格相等
	- `toBeCloseTo(number, numDigits?)`:  比較小數點值來避免誤差
	- `toEqual(value)`:  遞迴檢查object或array的每個值
	- 
	
------
## Testing Asynchronous Code (測試異步函數)
在測試異步函數時, JEST需要知道何時執行完成。在異步函數執行完成前JEST會去執行其他測試。
- 回調函數
默認情況下, JEST測試在執行到行尾即完成, 這表示在調用回調函數前測試已結束。
**解決方法**：在測試函數中接受一參數`done()`,  JEST會等待`done()`回調函數執行結束後結束測試, 若未被調用則執行失敗(顯示超時錯誤)
<br>
- Promises
在測試函數中**return** a Promise, JEST會等待resolve/catch
可使用`.resolve`/`.rejects` matchers
<br>
- Async / Await
可與`.resolve`/`.rejects`結合使用
