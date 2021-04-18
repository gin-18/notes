# canvas

canvas的width和height属性不要使用css设置，会失真变形。

```html
<canvas width="500" height="500"></canvas>
```

在代码添加以下代码可以在编写代码的时候得到补全

```
/** @type {HTMLCanvasElement} */
```

canvas.getContext()获取canvas的上下文。

fillStyle属性

fillRect属性，在页面中绘制矩形。fillRect属性一共4个值：x轴的偏移量，y轴的偏移量，宽度，高度。

图形一旦绘制成功就不能在修改。

如果需要让canvas图形移动，必须按照清屏-更新-渲染的逻辑进行。

## canvas中的3种绘制方式

stroke fill stroke&fill
