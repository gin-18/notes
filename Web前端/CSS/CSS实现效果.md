# CSS实现效果

---

## CSS属性书写顺序

CSS的书写应该遵循以下原则

> 1. 布局定位属性：display,position,float,clear,visibility,overflow（建议第一个写display，关系到模式）
> 2. 自身属性：width,height,margin,padding,border,background
> 3. 文本属性：color,font,text-decoration,text-align,vertical-align,white-space,break-word
> 4. 其他属性：content,cursor,border-radius,box-shadow,text-shadow,background:line-gradient...

---

## 清除内外边距

网页元素很多都带有默认的内外边距，而且不同的浏览器的默认值也不同。因此需要在布局时，清除网页元素的内外边距。

```css
* {
    padding: 0;
    margin: 0;
}
```

> * 行内元素为了照顾兼容性，尽量设置左右内外边距，不要设置上下内外边距。但是转换成块元素或行内块元素就可以了。

---

## 清除浮动

由于父级盒子很多情况下不方便给高度，但是子盒子浮动又不占位置，最后父级盒子高度为0时，就会影响下面的标准流盒子。

> * 清除浮动的本质就是清除浮动元素造成的影响。父级盒子有高度则不需要清除浮动。
> * 清除浮动之后，父级就会根据浮动的子盒子自动检测高度。父级有了高度就不会影响下面的标准流。

```css
选择器 {
    clear: 属性值;
}
```

| 属性值 | 作用                                       |
| ------ | ------------------------------------------ |
| left   | 不允许左则有浮动元素（清除左侧浮动的影响） |
| right  | 不允许右侧右浮动影响（清除右侧浮动的影响） |
| both   | 同时清除两侧浮动的影响                     |

在实际开发中，几乎只用==clear: both;==

### 清除浮动的方法

**额外标签法（隔墙法），W3C推荐使用**

> * 额外标签法就是在浮动元素末尾添加一个空标签。例如，&lt;div style="clear: both"&gt;&lt;/div&gt;，或者其他标签（&lt;br/&gt;）等。
> * 新添加的空标签必须是块元素，不能是行内元素。

**父级添加overflow属性**

> * 在父级元素中添加overflow属性，属性值可以设置为==hidden==，==auto==，==scroll==。

**父级添加after伪元素**

==:after==方式是额外标签法的升级版，也是给父元素添加。

```css
.clearfix:after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix {
    *zoom: 1;
}
```

**父级添加双伪元素**

```css
.clearfix:before,.clearfix:after {
    content: "";
    display: table;
}
.clear:after {
    clear: both;
}
.clear {
    *zoom: 1;
}
```

---

## 块级盒模型的水平居中显示

利用==外边距==可以实现块级盒模型的水平居中显示，但是必须满足两个条件。

> 1. 盒子必须设置width宽度。
> 2. 盒子左右外边距都设置为auto。
> 3. 如果需要让行内元素或行内块元素水平居中只需要给其父元素添加text-align:center即可。

---

## 圆角边框

CSS中新增了圆角边框样式，可以将盒子变为圆角的。

使用==border-radius==属性可以设置元素的外边框为圆角。

```css
border-radius：length；
```

radius半径原理：圆与边框的交集形成圆角效果。

> * 属性值可以用px单位表示也可以用百分比表示。
> * 将矩形设置为圆角矩形的方法：将属性值设置为盒子高度的一半。
> * 将正方形设置为圆形的方法：将属性值设置为宽度或高度的一半即可。
> * border-radius也可以简写，跟4个值的话，则分别表示左上角，右上角，右下角，左下角。

---

## 盒子阴影

使用==box-shadow==属性可以为盒子设置阴影。

```css
box-shadow: h-shadow v-shadow bulr spread color inset;
```

| 属性     | 作用                                 |
| -------- | ------------------------------------ |
| h-shadow | 必需属性，水平阴影的位置，允许负值。 |
| v-shadow | 必需属性，垂直阴影的位置，允许负值。 |
| bulr     | 可选，模糊距离。                     |
| spread   | 可选，阴影尺寸。                     |
| color    | 可选，阴影颜色。                     |
| inset    | 可选，将外部阴影设置为内部阴影。     |

> * 盒子不占用空间，不会影响其他盒子的排列。
> * 使用==:hover==可以设置鼠标经过时才显示阴影。

---

## 文本阴影

使用==text-shadow==可以为文本设置阴影

| 属性     | 作用                                 |
| -------- | ------------------------------------ |
| h-shadow | 必需属性，水平阴影的位置，允许负值。 |
| v-shadow | 必需属性，垂直阴影的位置，允许负值。 |
| bulr     | 可选，模糊距离。                     |
| color    | 可选，阴影颜色。                     |

---

## 元素的显示与隐藏

让一个元素在页面中显示或隐藏起来。

### display显示隐藏

> * display: none; 隐藏对象。
> * display: block; 除了转换块元素外，同时还有显示元素的作用。
> * 隐藏起来的元素不再占用原来的位置。

### visibility显示隐藏

visibility属性用于指定一个元素是可见还是隐藏。

> * visibility: visible; 元素可视。
> * visibility: hidden; 元素隐藏。
> * visibility隐藏元素之后，继续占用原来的位置。

### overflow溢出

overflow属性对溢出部分的显示与隐藏。

| 属性值  | 作用                                   |
| ------- | -------------------------------------- |
| visible | 不剪切内容也不添加滚动条               |
| hidden  | 隐藏超出的部分                         |
| scroll  | 总是显示滚动条                         |
| auto    | 溢出时显示滚动条，不溢出时不显示滚动条 |

---

## 精灵图（sprites）

为了减少服务器的接收和发送请求的次数，提高页面加载的速度。

核心原理：页面中一些小的背景图片整合到一张大的图片中，这样服务器只需要处理一次请求就可以了。

### 精灵图的使用

使用精灵图的核心

> * 精灵图主要是针对背景图片的。就是将多个小背景图片整合到一张大的图片中。
> * 移动背景图片位置，此时可以使用background-position。
> * 移动的距离就是这个目标图片的x坐标和y坐标。

---

## 字体图标（iconfont）

字体图标的使用场景：主要用于网页中通用，常用的小图标。

字体图标可以为前端工程师提供一种方便高效的图标使用方式，展示的是图标，实际是字体。

### 字体图标的下载

推荐网站

www.icomoon.com

www.iconfont.cn

---

## 实现CSS三角形

> * 盒子宽度，高度设置为0。为了照顾兼容性line-height和font-size也都设置为0。
> * 三个边框值设置为透明。
> * 剩下一个边框值不透明。

---

## 鼠标样式（cursor）

| 属性值      | 作用         |
| ----------- | ------------ |
| default     | 小白（默认） |
| pointer     | 小手         |
| move        | 移动         |
| text        | 文本         |
| not-allowed | 禁止         |

---

## 去除表单元素的轮廓线

给表单添加outline: 0;或outline: none;样式可以去掉默认的轮廓线。

```css
input {
    outline: none;
}
```

---

## 防止拖拽文本域（resize）

```css
textarea {
    resize: none;
}
```

---

## vertical-align属性

使用场景：设置图片或表单（行内块元素）和文本的垂直对齐。只针对行内元素或行内块元素生效。

语法：

```css
vertical-align: baseline | top | middle | bottom
```

| 属性值   | 作用                                   |
| -------- | -------------------------------------- |
| baseline | 默认，元素放在父元素的基线上           |
| top      | 把元素的顶端与行中最高元素的顶端对齐   |
| middle   | 把此元素放在父元素的中部               |
| bottom   | 把元素的顶端与行中最低的元素的顶端对齐 |

---

## 解决图片底部默认空白缝隙问题

图片底部会有一个空白缝隙，原因是行内块元素会和文本的基线对齐。

解决方法

> * 给图片添加vertical-align属性。（提倡使用）
> * 将图片转换成块元素display: block;

---

## 溢出文本的省略号显示

单行文本溢出的省略号显示必须满足三个条件

> 1. 先强制一行内显示文本。（white-space: nowrap;）
> 2. 超出的部分隐藏。（overflow: hidden;）
> 3. 溢出文本用省略号代替。（text-overflow: ellipsis;）

多行文本溢出的省略号显示

适用于webkit浏览器或移动端。

```css
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;（弹性伸缩盒子模型显示）
-webkit-line-clamp: 2;（限制在一个块元素显示的文本行数）
-webkit-box-orient: vertical;（设置或检索伸缩盒对象的子元素的排列方式）
```

---

## CSS初始化

不同浏览器对某些标签的默认值是不同的，为了消除不同浏览器对HTML文本呈现的差异，照顾浏览器的兼容性，需要对CSS初始化。CSS初始化就是重新设置浏览器的样式（CSS reset）