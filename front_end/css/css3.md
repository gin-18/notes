# CSS3

**W3School的CSS3教程**：https://www.w3school.com.cn/css3/index.asp

## CSS3模块

CSS3被划分为模块，其中重要的CSS模块包括：

```
* 选择器
* 盒模型
* 背景和边框
* 文本效果
* 2D/3D转换
* 动画
* 多列布局
* 用户界面
```

## 浏览器前缀

浏览器内核通常也称为渲染引擎。

针对旧的浏览器兼容性，添加不同的浏览器前缀。

| 浏览器        | 内核    | 前缀     |
|---------------|---------|----------|
| IE            | Trident | -ms-     |
| FireFox       | Gecko   | -moz-    |
| Oprea         | Presto  | -o-      |
| Chrome        | Webkit  | -webkit- |
| Safari        | Webkit  | -webkit- |
| Oprea, Chrome | Blink   |          |

## 渐变(gradient)

渐变就是两种颜色的平滑过度。

### 色标

在创建渐变的过程中，可以指定多个中间颜色值，这个值就称为色标。每个色标包含一种颜色和一个位置，

常用于`background-image`

### 线性渐变

```
background-image: line-gradient([[<angle> | to <side-or-corner> ], ]?<color-stop>[,<color-stop>]+);
```

#### angle 

通过角度来确实渐变的方向。0读度表示渐变方向从下向上，90度表示渐变方向从左向右

#### side-or-corner

通过关键词来确定渐变方向。比如`to top`，`to right`，`to bottom`，`to left`。对角线可以写`to left top`。

#### color-stop

表示颜色的起始点和颜色的结束点。

### 径向渐变

```
background-image: radial-gradient([[<shape> || <size> [at <position>]?,| at <position>,]?<color-stop>[,<color-stop>]+);
```

#### position

定义径向渐变的圆心位置。类似于background-position。默认值是center。

#### shape

主要用来定义渐变的形状。主要包括两个值：`circle`，`ellipse`。

```
circle：如果<size>和<length>大小相等，径向渐变是一个圆。

ellipse：如果<size>和<length>大小不相等，径向渐变是一个椭圆。
```

#### size

定义径向渐变结束形状的大小。默认值是farther-corner。

```
closest-side：指定径向渐变的半径长度为从圆心到离圆心最近的边。

closest-corner：指定径向渐变的半径长度为从圆心到离圆心最近的角。

farther-side：指定径向渐变的半径长度为从圆心到离圆心最远的边。

farther-corner：指定径向渐变的半径长度为从圆心到离圆心最远的角。
```

#### color-stop

径向渐变上停止的颜色。

### 重复线性渐变

repeating-line-gradient

repeating-radial-gradient

## 变形(transform)

transform属性指一组转换函数。

transform-origin属性指定元素的中心点。

transform-origin-z控制元素三维空间的中心点。

transform-style的值为`preserver-3d`，建立一个3D渲染环境。

```
transform: none | <transform-function> [<transform-function>]
```

### transform-function(2D)

| 函数        | 描述                                                                           |
|-------------|--------------------------------------------------------------------------------|
| translate() | 移动元素，可以根据x轴和y轴重新定义元素位置。扩展函数translateX()和translateY() |
| scale()     | 缩小或放大元素，扩展函数scaleX()和scaleY()                                     |
| rotate()    | 旋转元素                                                                       |
| skew()      | 元素倾斜，扩展函数skewX()和skewY()                                             |
| matrix()    | 定义矩阵变形                                                                   |

### transform-function(3D)

| 函数                            | 描述                       |
|---------------------------------|----------------------------|
| translate3d()                   | 移动元素                   |
| translate()                     | 指定3D位移在z轴的位移量    |
| scale3d()                       | 缩放元素                   |
| scaleZ()                        | 指定z轴的缩放向量          |
| rotate3d()                      | 指定元素具有三维旋转的角度 |
| rotateX()，rotateY()，rotateZ() | 旋转元素                   |
| perspective()                   | 指定透视投影矩阵           |
| matrix3d()                      | 定义矩阵变形               |

### transform-origin

```
transform-origin: 
```

## 过度(transition)

```
transition: [<transition-property> || <transition-duration>]
```

## 动画(animation)

### 关键帧(@keyframes)

```
@keyframes IDENT {
  from {
    // css
  }
  percentage {
    // css
  }
  to {
    // css
  }
}

或

@keyframes IDENT {
  0% {
    // css
  }
  25% {
    // css
  }
  100% {
    // css
  }
}
```

animation属性一个有8个子属性。

```
animation: [<animation-name> || <animation-duration> || <animation-timing-function> || <animation-delay> || <animation-iteration-count> || <animation-direction> || <animation-play-state> || <animation-fill-mode>]
```

| 属性                      | 描述                           |
|---------------------------|--------------------------------|
| animation-name            | 定义动画的名字                 |
| animation-duration        | 设置动画播放所需时间，以秒单位 |
| animation-timing-function | 设置动画的播放方式             |
| animation-delay           | 设置动画开始时间，以秒为单位   |
| animation-iteration-count | 设置动画循环次数               |
| animation-direction       | 设置动画播放方向               |
| animation-play-state      | 控制动画的播放状态             |
| animation-fill-mode       | 设置动画的时间外属性           |


### animation-name

animation-name定义动画的名称。none表示没有动画。IDENT调用@keyframes关键帧定义的动画。

```
animation-name: none | IDENT[,none|IDENT];
```


### animation-duration

设置动画播放时间。

```
animation-duration: <time>[,<time>]
```

### animation-timing-function(？？？)

设置动画的播放方式。

```
animation-timing-function: ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>)
```

### animation-delay

定义动画开始执行前等待的时间。

```
animation-delay: <time>[,<time>]
```

### animation-iteration-count

定义动画播放的次数。

属性值通常为整数，infinite动画将无限次执行。

```
animation-iteration-count: infinite | <number>
```

### animation-direction

设置动画的播放方向。

```
animation-direction: normal | alternate
```

默认值为normal，alternate为偶数次正向播放，奇数次反向播放。

### animation-play-state

控制动画的播放状态。

```
animation-play-state: running | paused
```

默认值为running，paused停止动画。

### animation-fill-mode

定义动画开始之前和结束之后的操作。

```
animation-fill-mode: none | forwards | backwards | both
```

默认值为none

forwards应用动画最后一帧的位置

backwards应用动画初始帧的位置

both同时具有forwards和backwards的效果





















## CSS3动画

==animation==可以通过设置多个节点来精准控制一个或一组动画，来实现复杂的动画效果。

**动画的基本使用**

> 1. 先定义好动画。
> 2. 再调用动画。

**==keyframes==定义动画(类似定义类选择器)**

```css
@keyframes 动画名称 {
    0% {
        width: 100px;
    }   
    100% {
        width: 100px;
    }
}
```

> * 0%是动画的开始，100%是动画的结束。这样的规则称为动画序列。
> * 在keyframes中定义某项CSS样式，就能创建由当前样式逐渐改变为新样式的动画效果。
> * 动画是使元素从一种样式逐渐转换成另一种样式的效果，可以改变任意多的样式的任意多次。
> * 可以使用from和to代替百分号，两者效果相同。但是百分比是动画时长的划分。

**调用动画**

```css
/*调用动画*/
animation-name: 动画名称;
/*持续时间*/
animation-duration: 持续时间;
```

**动画常用属性**

| 属性                      | 描述                                                         |
| ------------------------- | ------------------------------------------------------------ |
| @keyframes                | 规定动画。                                                   |
| animation                 | 所以动画属性的简写，除了animation-play-state。               |
| animation-name            | 规定keyframes动画的名称。必要属性。                          |
| animation-duration        | 规定动画完成一个周期所花费的时间（秒数或毫秒数），默认是0。必要属性。 |
| animation-timing-function | 规定动画的运动曲线，默认是ease。                             |
| animation-delay           | 规定动画何时开始，默认是0。                                  |
| animation-iteration-count | 规定动画被播放的次数，默认是1，还有infinite。                |
| animation-direction       | 规定动画是否在下一个周期逆向播放，默认是normal，逆播放是alternate。 |
| animation-play-state      | 规定动画是否正在运行或暂停，默认是running，还有paused。      |
| animation-fill-mode       | 规定动画结束后的状态，保持forwards回到起始backwards。        |

---

## 3D转换

网页的三维坐标系有：==x轴==，==y轴==，==z轴==。

x轴：水平向右。x右边是正值，左边是负值。

y轴：垂直向下。y下面是正值，上面是负值。

z轴：垂直屏幕。往外是正值，往里是负值。

### 3D移动

3D移动在2D移动的基础上增加了在z轴方向上的移动。

| 属性               | 描述                                        |
| ------------------ | ------------------------------------------- |
| translateX(n)      | 仅在x轴上移动相应的距离                     |
| translateY(n)      | 仅在y轴上移动相应的距离                     |
| translateZ(n)      | 仅在z轴上移动相应的距离，且单位一般都使用px |
| translate3d(x,y,z) | 分别在x，y，z轴上移动相应的距离             |

==perspective==(透视)

透视写在被观察元素的父盒子上面。

d：视距。视距就是人眼到屏幕的距离。

z：z轴。物体距离屏幕的距离，z轴正值越大，看到的物体就越大。

### 3D旋转

| 属性                | 描述                   |
| ------------------- | ---------------------- |
| rotateX(45deg)      | 沿着x轴正方向旋转45deg |
| rotateY(45deg)      | 沿着y轴正方向旋转45deg |
| rotateZ(45deg)      | 沿着z轴正方向旋转45deg |
| rotate3d(x,y,z,deg) | 沿着自定义轴旋转       |

### 3D呈现

==transform-style==控制着子元素是否开启三维立体环境。

> * transform-style: flat; 子元素不开启3D立体空间（默认值）。
> * transform-style: preserve-3d; 子元素开启3D立体空间。
> * 代码写在父级盒子中。
> * 很重要的属性。
































