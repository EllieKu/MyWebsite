# SVG   --2020/07/19
- `<svg></svg>`

## shape
 - `<rect>` - Rectangle
 - `<circle>` - Circle
 - `<ellipse>` - Ellipse
 - `<line>` - Line
 - `<polyline>` - Polyline
 - `<polygon>`- Polygon
 - `<Path>` - Path
 - `<text>` 
 
 ## attribute
attribute | description | value | note
----------|-------------|-------|-----
width | width | 100 | 
height | height | 120 |
fill | the fill color | rgb(0,0,255)
stroke | color of the border | rgb(0,0,255)
stroke-width | width of the border | 3 
cx | the x coordinates of the center of the circle | 20 | `<circle>` `<ellipse>`
cy | the y coordinates of the center of the circle | 20 | `<circle>` `<ellipse>`
r | radius of the circle | 10 | `<circle>` `<ellipse>`
rx | the horizontal radius | 8 | `<ellipse>`
ry | the vertical radius | 4 | `<ellipse>`
x1 | the start of the line on the x-axis | 0 | `<line>`
y1 | the start of the line on the y-axis | 0 | `<line>`
x2 | the start of the line on the x-axis | 200 | `<line>`
y2 | the start of the line on the y-axis | 200 | `<line>`
points |  the x and y coordinates for each corner | 200,10 250,190 160,210 | `<polygon>`
fill-rule | determine the inside part of a shape |	nonzero/evenodd | `<path>`、`<polygon>`、`<polyline>`
M/L |

## 參考資料
1. [SVG Attribute reference](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute)