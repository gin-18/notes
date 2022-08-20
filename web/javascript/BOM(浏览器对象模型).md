# BOM

BOM就是浏览器对象模型，BOM提供了与浏览器窗口进行交互的对象，BOM的核心对象是window。

## 窗口加载事件

window.onload是窗口加载事件，当文档内容完全加载才会触发的事件(图像，脚本文件，css文件)。

```
window.onload = function() {}

或

window.addEventListener("load", function() {});
```

DOMContentLoaded事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等。

```
document.addEventListener("DOMContentLoaded", function() {})
```

## 窗口大小事件

window.resize是调整窗口大小加载事件，当触发时就调用处理函数。

```
window.onresize = function() {}

或

window.addEventListener("resize", function() {});
```

## 定时器

window对象提供了2种定时器。

```
setTimeout()

setInterval()
```

### setTimeout()定时器

只调用一次回调函数。

```
window.setTimeout(callback, [延迟的毫秒数])
```

### setInterval()定时器

setInterval()方法可以重复调用一个函数，每间隔这个时间，就会调用一次回调函数。

```
setInterval(callback, [延迟的毫秒数])
```

## 清除定时器

ClearInterval()方法取消之前调用的setInterval()创建的定时器。

```
window.clearInterval(intervalID)
```

## location对象

window对象中的location属性用于获取或设置窗体的URL，并可以用于解析URL。location属性会返回一个对象，所以也称为location对象。

### location对象的属性

| 属性              | 描述                                    |
|-------------------|-----------------------------------------|
| location.href     | 获取或设置整个URL                       |
| location.host     | 返回主机                                |
| location.port     | 返回端口号                              |
| location.pathname | 返回路径                                |
| location.search   | 返回参数                                |
| location.hash     | 返回片段，#后面的内容，常见于链接，锚点 |

重点：href, search

## URL

URL就是同意资源定位符。

```
protocol://host[:port]/path/[?query]#fragment
```

| 组成     | 描述                             |
|----------|----------------------------------|
| protocol | 通信协议，常用的http，ftp，maito |
| host     | 主机(域名)                       |
| port     | 端口号                           |
| path     | 路径                             |
| query    | 参数                             |
| fragment | 片段                             |

## javascript animation

核心原理：通过定时器setInterval()不断移动盒子的位置。

盒子必须加定位。












