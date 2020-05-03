# canvas 學習  2020/05/03

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
* [Path2D()](https://developer.mozilla.org/zh-CN/docs/Web/API/Path2D/Path2D) 讓我們可以快取和記錄繪圖指令，方便快速重複地繪圖

## 樣式
### 顏色
* `fillStyle = color` --顏色填滿圖形
* `strokeStyle = color` --顏色勾勒圖形
* `globalAlpha = transparencyValue` --透明度-0.0(全透明)~1.0(不透明)。一旦設定畫布上所有圖形的不透明度都會套用此設定值。預設值為1.0
    由CSS3顏色值能夠指定不透明度，我們也可以如下面一般，設定strokeStyle以及fillStyle來變更不透明度。
    ```js
    // Assigning transparent colors to stroke and fill style`
    ctx.strokeStyle = "rgba(255,0,0,0.5)";
    ctx.fillStyle = "rgba(255,0,0,0.5)";    
    ```
### [線條樣式](https://developer.mozilla.org/zh-TW/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors)
* `lineWidth = value` --線條寬度
* `lineCap = type` --線條結尾樣式,下列為type值:
* `lineJoin = type` --線條和線條間接合處的樣式
* `miterLimit = value` --限制當兩條線相交時交接處最大長度；所謂交接處長度(miter length)是指線條交接處內角頂點到外角頂點的長度


---

待續
