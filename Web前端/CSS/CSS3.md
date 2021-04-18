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

## 2D转换

`transform`可以实现元素的位移，旋转，缩放等效果。

| 属性      | 描述 |
| --------- | ---- |
| translate | 移动 |
| rotate    | 旋转 |
| scale     | 缩放 |

==translate==(移动)可以改变元素在页面中的位置。

```css
transform: translate(x,y);
transform: translateX(n);
transform: translateY(n);
```

> * translate不会影响其他盒子的位置。
> * translate中的百分比单位是相对于自身元素的百分比。
> * 对行内标签没有效果。

==rotate==(旋转)可以让元素按顺时针或逆时针旋转。

```css
transform: rotate(度数);
```

> * rotate中跟的是度数，单位是deg。例：rotate(45deg)。
> * 角度是正时，按顺时针旋转；角度是负时，按逆时针旋转。
> * 默认的旋转中心点是元素的中心点。

==transform-origin==可以设置元素旋转的中心点。

```css
transform-origin: x y;
```

> * 后面的参数x和y用分号隔开。
> * x和y默认旋转的中心点是元素的中心点(50% 50%)。
> * 还可以给x和y设置像素或方位名词(top，bottom，left，right，center)。

==scale==(缩放)可以控制元素的大小。

```css
transform: scale(x,y);
```

> * x和y填的是数字，表示倍数，不要跟单位。
> * scale可以设置中心点，默认中心点是元素的中心点，而且不影响其他的盒子。

---

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

## 渐变(grandients)

渐变就是两种颜色的平滑过度

### 色标

在创建渐变的过程中，可以指定多个中间颜色值，这个值就称为色标。每个色标包含一种颜色和一个位置，
