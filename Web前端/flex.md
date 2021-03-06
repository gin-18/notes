# Flex布局

在flex布局中，父盒子称为flex container，子盒子称为flex item。

1. 块级布局侧重垂直方向，行内布局侧重水平方向，flex布局则与方向无关。
2. flex布局可以实现空间自动分配，自动对齐。
3. flex布局适用于简单的线性布局，更复杂的布局要交给grid布局。

## flex container的属性

| 属性            | 描述                            |
|-----------------|---------------------------------|
| flex-direction  | 方向                            |
| flex-wrap       | 换行                            |
| flex-flow       | flex-direction和flex-wrap的简写 |
| justify-content | 主轴方向的对齐方式              |
| align-items     | 侧轴方向的对齐方式              |
| align-content   | 多行/列内容的对齐方式           |

### flex-direction属性
