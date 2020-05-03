# canvas 學習  2020/05/03

* 沒有src和alt屬性，只有width(預設300px)和height(預設150px)

* 不支援<canvas>的瀏覽器看到不認識的<canvas>時會忽略<canvas>，而此時在<canvas>下瀏覽器認識的替代內容則會被瀏覽器解析顯示，
 至於支援<canvas>的瀏覽器則是會正常解析<canvas>，忽略替代內容。

 ## 支援性檢查
```
var canvas = document.getElementById('tutorial');

if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```
