# canvas 學習  2020/05/03
[Canvas教學文件](https://developer.mozilla.org/zh-TW/docs/Web/API/Canvas_API/Tutorial)

* 沒有src和alt屬性，只有width(預設300px)和height(預設150px)
* 不支援<canvas>的瀏覽器看到不認識的<canvas>時會忽略<canvas>，而此時在<canvas>下瀏覽器認識的替代內容則會被瀏覽器解析顯示，
 至於支援<canvas>的瀏覽器則是會正常解析<canvas>，忽略替代內容。

## 支援性檢查

```js
var canvas = document.getElementById('tutorial');
if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```

## 畫矩形
* `fillRect(x, y, width, height)` --填滿的矩形
* `strokeRect(x, y, width, height)` --矩形的邊框
* `clearRect(x, y, width, height)` --清除指定矩形區域內的內容，使其變為全透明

## 路徑繪製
* `beginPath()` --開始新路徑，再使用繪圖指令設定路徑
* `closePath()` --關閉路徑

### 繪圖指令 ([路徑API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_usage))
* `stroke()` --畫出圖形邊框
* `fill()` --填滿路徑內容
* `moveTo(x,y)` --移動畫筆到(x,y)座標點
* `lineTo(x,y)` --從目前繪畫點畫一直線到(x,y)座標點
* `arc(x, y, radius, startAngle, endAngle, anticlockwise)` --畫弧形
    - x, y代表圓心座標點
    - radius代表半徑
    - startAngle, endAngle分別代表沿著弧形曲線上的起始點與結束點的弧度，弧度測量是相對於x軸，
    - anticlockwise為true代表逆時針作圖、false代表順時針作圖(option)
* `quadraticCurveTo(cp1x, cp1y, x, y)` --弧形(二次貝茲曲線),從目前起始點畫一條**二次貝茲曲線**到x, y指定的終點，控制點由cp1x, cp1y指定
* `bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)` --弧形(三次貝茲曲線),從目前起始點畫一條 **三次貝茲曲線**到x, y指定的終點，控制點由(cp1x, cp1y)和  `(cp2x, cp2y)指定
* ![Bezier curve](https://media.prod.mdn.mozit.cloud/attachments/2012/07/09/223/c6ec7dd953e455094b46f514ba24680c/Canvas_curves.png)
* `rect(x, y, width, height)` --矩形,左上角位於(x, y)、寬width、高height

### Path2D Object
* [Path2D( )](https://developer.mozilla.org/zh-CN/docs/Web/API/Path2D/Path2D) 讓我們可以快取和記錄繪圖指令，方便快速重複地繪圖

## 樣式
### 顏色
* `fillStyle = color` --顏色填滿圖形
* `strokeStyle = color` --顏色勾勒圖形
* `globalAlpha = transparencyValue` --透明度 0.0~1.0(預設)。
  <p>設定後畫布上所有圖形的都會套用此設定值。能由CSS3指定不透明度，亦可如下設定strokeStyle以及fillStyle來變更不透明度。</p>
    ```js
    // Assigning transparent colors to stroke and fill style`
    ctx.strokeStyle = "rgba(255,0,0,0.5)";
    ctx.fillStyle = "rgba(255,0,0,0.5)";    
    ```
  
### [線條樣式](https://developer.mozilla.org/zh-TW/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors)
* `lineWidth = value` --線條寬度 
* `lineCap = type` --線條結尾 (butt/round/square)
* `lineJoin = type` --線條和線條間接合處 (round/bevel/mite?)
* `miterLimit = value` --限制當兩條線相交時交接處最大長度；所謂交接處長度(miter length)是指線條交接處內角頂點到外角頂點的長度


---

待續

---
## 狀態保存
* `save()` --保存畫布所有狀態(樣式和變形設定)
* `restore()` --恢復上一次畫布狀態

## 移動
* `translate(x, y)` --x 是左右偏移量，y 是上下偏移量
* `` 
* `` 
* `` 
待續
---
## 動畫
### 基本步驟
1. **清除畫布** --除了不變的背景畫面，所有先前畫的圖案都要先清除，這個步驟可以透過clearRect()方法達成。
2. **儲存畫布狀態** --若是想要每一次重新繪圖時畫布起始狀態都是原始狀態，那麼就需要先行儲存畫布原始狀態。
3. **畫出畫面** --畫出需要畫面。
4. **復原畫布狀態** --復原畫布狀態以備下次繪圖使用。

### 控制動畫
一般來說當程式碼執行完畢後我們才會看到繪圖結果，所以說我們無法靠執行for迴圈來產生動畫，我們得靠每隔一段時間繪圖來產生動畫，下面將介紹兩種作法。
#### 排程更新
* `setInterval(function, delay)` 
* `setTimeout(function, delay)` 
* `requestAnimationFrame(callback)` --告訴瀏覽器你希望執行動畫的時候,要求瀏覽器在重繪下一張畫面之前,呼叫callback函數來更新動畫
#### 從使用者輸入操作控制動畫(EventListener)
* `` 

