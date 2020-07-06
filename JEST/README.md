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
默認情況下, JEST測試在執行到行尾即完成, 這表示在調用回調函數前測試已結束。<br>
**解決方法**：在測試函數中接受一參數`done()`,  JEST會等待`done()`回調函數執行結束後結束測試, 若未被調用則執行失敗(顯示超時錯誤)
<br>
- Promises
在測試函數中**return** a Promise, JEST會等待resolve/catch
可使用`.resolve`/`.rejects` matchers
<br>
- Async / Await
可與`.resolve`/`.rejects`結合使用

--------
## Setup and Teardown
在測試開始前或結束後的執行工作
- `beforeEach()`/`afterEach()`: 在**每個**測試函數前/後執行 (Repeating Setup For Many Tests)
- `beforeAll()`/`afterAll()`: 在**全部**測試函數前/後執行一次 (One-Time Setup)
- 
 ### Scoping
*before*和*after*的作用域default = global，利用`describe` 可以將其作用block於函數內<br>
**注意**: 全域*beforeEach* 比`describe`內的*beforeEach*早執行
```
beforeAll(() => console.log('1 - beforeAll'));	// 1
afterAll(() => console.log('1 - afterAll'));	// 12
beforeEach(() => console.log('1 - beforeEach'));	// 2. 6
afterEach(() => console.log('1 - afterEach'));	// 4. 10
test('', () => console.log('1 - test'));	// 3
describe('Scoped / Nested block', () => {
  beforeAll(() => console.log('2 - beforeAll'));    // 5
  afterAll(() => console.log('2 - afterAll'));    // 11
  beforeEach(() => console.log('2 - beforeEach'));    // 7
  afterEach(() => console.log('2 - afterEach'));   // 9
  test('', () => console.log('2 - test'));    // 8
});
```
### Order of execution of describe and test blocks (describe和test塊的執行順序)
所有`describe`handlers會比實際測試先執行。JEST預設情況下，當所有`describe`執行完成，依序執行`test`且等待完成才會執行下一個（Once the describe blocks are complete, by default Jest runs all the tests serially in the order they were encountered in the collection phase, waiting for each to finish and be tidied up before moving on）
```
describe('outer', () => {
  console.log('describe outer-a');    // 1

  describe('describe inner 1', () => {
    console.log('describe inner 1');    // 2
    test('test 1', () => {
      console.log('test for describe inner 1');    // 6
      expect(true).toEqual(true);
    });
  });

  console.log('describe outer-b');    // 3

  test('test 1', () => {
    console.log('test for describe outer');    // 7
    expect(true).toEqual(true);
  });

  describe('describe inner 2', () => {
    console.log('describe inner 2');    // 4
    test('test for describe inner 2', () => {
      console.log('test for describe inner 2');    // 8
      expect(false).toEqual(false);
    });
  });

  console.log('describe outer-c');    // 5
});
```
