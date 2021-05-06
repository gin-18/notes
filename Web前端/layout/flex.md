# Flex布局

在flex布局中，父盒子称为`flex container`，子盒子称为`flex item`。

## flex container的属性

| 属性              | 描述                                |
|-------------------|-------------------------------------|
| `flex-direction`  | 设置主轴方向                        |
| `flex-wrap`       | 换行                                |
| `flex-flow`       | `flex-direction`和`flex-wrap`的简写 |
| `justify-content` | 主轴方向的对齐方式                  |
| `align-items`     | 侧轴方向的对齐方式                  |
| `align-content`   | 多行/列内容的对齐方式               |

### flex-direction

---

`flex-direction`属性定义主轴方向。

```css
flex-direction: row | row-reverse | column | column-reverse;
```

| 属性值           | 描述             |
|------------------|------------------|
| `row`            | 默认值，水平向右 |
| `row-reverse`    | 水平向左         |
| `column`         | 垂直向下         |
| `column-reverse` | 垂直向上         |

### flex-wrap

---

如果一行排不下，则换行。

```css
flex-wrap: nowrap | wrap | wrap-reverse;
```

| 属性值         | 描述               |
|----------------|--------------------|
| `nowrap`       | 默认值，不换行     |
| `wrap`         | 换行，第一行在上方 |
| `wrap-reverse` | 换行，第一行在下方 |

### flex-flow

---

`flex-direction`属性和`flex-wrap`属性的简写。

```css
flex-flow: <flex-direction> | <flex-wrap>
```

### justify-content

---

`justify-content`属性定义项目在主轴上的对齐方式。

```
justify-content: flex-start | flex-end | center | space-between | space-around;
```

| 属性值          | 描述                                                               |
|-----------------|--------------------------------------------------------------------|
| `flex-start`    | 默认值，左对齐                                                     |
| `flex-end`      | 右对齐                                                             |
| `center`        | 居中                                                               |
| `space-between` | 两端对齐，项目之间的间隔相等                                       |
| `space-around ` | 每个项目两侧的间隔相等，所以项目之间的间隔比项目与边框的间隔大一倍 |

### align-items

---

`align-items`属性定义项目在侧轴上的对齐方式。

`flex container`需要有高度。

```css
align-items: flex-start | flex-end | center | baseline | stretch;
```

| 属性值       | 描述                                                     |
|--------------|----------------------------------------------------------|
| `flex-start` | 侧轴的起点对齐                                           |
| `flex-end`   | 侧轴的终点对齐                                           |
| `center`     | 侧轴的中点对齐                                           |
| `baseline`   | 项目的第一行文字的基线对齐                               |
| `stretch`    | 默认值，如果项目未设置高度或为auto，将占满整个容器的高度 |


### align-content

---

`align-content`属性定义了多根轴线的对齐方式，如果项目只有一根轴线，该属性不起作用。

```css
align-content: flex-start | flex-end | center | space-between | space-around |stretch;
```

| 属性值          | 描述                                                                   |
|-----------------|------------------------------------------------------------------------|
| `flex-start`    | 与侧轴的起点对齐                                                       |
| `flex-end`      | 与侧轴的终点对齐                                                       |
| `center`        | 与侧轴的中点对齐                                                       |
| `space-between` | 与侧轴两端对齐，轴线之间的间隔平均分布                                 |
| `space-around`  | 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍 |
| `stretch`       | 默认值，轴线占满整个侧轴                                               |

## flex items的属性

| 属性          | 描述                                             |
|---------------|--------------------------------------------------|
| `order`       | 项目排列顺序                                     |
| `flex-grow`   | 项目放大比例                                     |
| `flex-shrink` | 项目缩小比例                                     |
| `flex-basis`  | 分配剩余的空间                                   |
| `flex`        | flex-grow，flex-shrink，flex-basis三个属性的简写 |
| `align-self`  | 允许单个项目拥有不同的对齐方式                   |

### order

---

`order`属性定义项目的排列顺序。属性值为`整数`，数值小的在前面。

```css
order: <整数>
```

### flex-grow

---

`flex-grow`属性定义项目的放大比例。属性值为`数字`，默认值为0。

```css
flex-grow: <数字>
```

### flex-shrink

---

`flex-shrink`属性定义了项目的缩小比例。属性值为`数字`，默认值为1。

```css
flex-shrink: <数字>
```

### flex-basis

`flex-basis`属性定义了项目分配的剩余空间。属性值为`长度单位`，默认值为auto。

```css
flex-basis: <长度>
```

### align-self

`align-self`属性定义了项目可以拥有不同于其他项目的对齐方式。

```css
align-self: auto | flex-start | flex-end | center | baseline | stretch;
```







































