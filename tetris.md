# 俄罗斯方块

## 俄罗斯方块基准(tetris guideline)

文档：[俄罗斯方块基准](https://tetris.wiki/Tetris_Guideline)

### 必要规则

#### 场地(playfield)

必须10x20，条件允许可以显示21,22行的隐形缓冲区。

#### 方块初始方向

方块出现在21和22行，生成时平坦的一面朝下，出现后立即向下移动。

#### 方块颜色

| 形状  | I     | J     | L     | O     | S     | Z     | T     |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 颜色  | 淡蓝  | 深蓝  | 橙色  | 黄色  | 绿色  | 红色  | 紫色  |

#### 预览块

显示玩家将要摆放的方块。

#### 阴影块

阴影块可以帮助玩家判断方块将要下落的位置，有时，玩家可以通过设置关闭阴影块。

#### 暂存块

<++>

#### 超级旋转系统 SRS

<++>

#### 包随机生成器

<++>

#### 按键控制

##### 电脑标准按键设置

| 按键            | 左右键          | 上键            | 下键            | 空格            | C / Shift       | Z / 左Ctrl      |
| --------------- | --------------- | --------------- | --------------- | --------------- | --------------- | --------------- |
| 描述            | 移动            | 顺时针旋转90度  | 软降            | 硬降            | 暂存            | 逆时针旋转90度  |

#### 术语表

用户手册中必须使用 `tetriminos` 或 `tetrominos` 。

#### 速度表

文档：[马拉松](https://tetris.wiki/Marathon)

马拉松的速度曲线基于 Tetris Worlds 的马拉松模式。

方块下落一格的时间满足以下公式：

```latex
time = (0.8 - (level - 1) * 0.007)^(level-1)
```

#### 关卡

通过消行升级，每消除10行升一级。

#### 锁定延迟

<++>

#### 得分

文档：[Scoring](https://tetris.wiki/Scoring#Recent_guideline_compatible_games)

使用 tetris.com 的得分系统。

| Action                             | Points                                                 |
|------------------------------------|--------------------------------------------------------|
| Single                             | 100 x level                                            |
| Double                             | 300 x level                                            |
| Triple                             | 500 x level                                            |
| Tetris                             | 800 x level                                            |
| Mini T-Spin no line(s)             | 100 x level                                            |
| T-Spin no line(s)                  | 400 x level                                            |
| Mini T-Spin Single                 | 200 x level                                            |
| T-Spin Single                      | 800 x level                                            |
| Mini T-Spin Double (if present)    | 400 x level                                            |
| T-Spin Double                      | 1200 x level                                           |
| T-Spin Triple                      | 1500 x level                                           |
| Back-to-Back difficult line clears | Action score x 1.5 (excluding soft drop and hard drop) |
| Combo                              | 50 x combo count x level                               |
| Soft drop                          | 1 per cell                                             |
| Hard drop                          | 2 per cell                                             |

#### T-Spin 判断

1. T块的最后一个行为是旋转。

2. 以T块的中心块为中心所在的3x3的方格，这个3x3方格的4角中有3个方块被占用，这3个被占用的方块中，有2个在T块的前部，1个在T块的后部。

3. Mini T-Spin则是指在3个被占用的方块中，有1个在T块的前部，2个在T块的后部；但是，如果旋转是触发了踢墙，则仍然是T-Spin。

#### 背靠背(back-to-back)

连续两次或以上的消行都是“高级的消行”，其中“消四”和“T旋”被视为高级消行。

#### 连击(combo)

使用方块连续消行，即前一个方块消行，后一个方块也消行。

#### 终局条件

以下3种情况下，游戏结束：

* 当生成的方块与现有方块重叠

* 方块锁定时完全处于在场地的可见部分之外

* 或是方块被推出20格高的缓冲区

## 游戏模式

### 马拉松(Marathon)

经典的俄罗斯方块游戏。

### 竞速(Sprint or 40 Line)

尽量快的消除40行。

* 恒定下落速度
* 不记分数

### 限时打分(Ultra)

规定时间内获得尽量高的分数。

* 恒定下落速度(暂定)
* 不记分数















