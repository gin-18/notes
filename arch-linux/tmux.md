# tmux

## 会话与进程

在终端窗口输入命令,用户与计算机的这种临时的交互,称为一次"会话"

会话的一个重要特点是,窗口与其中启动的进程是连在一起的.打开窗口,会话开始;关闭窗口,会话结束.会话内部的进程也会终止.

为了解决这个问题,会话与窗口可以"解绑":窗口关闭时,会话不会终止,而是继续运行,等到以后需要的时候,再让会话"绑定"窗口

## tmux的作用

```
1. tmux允许在单个窗口中,同时访问多个会话

2. tmux可以让新窗口"接入"已经存在的会话

3. tmux允许每个会话有多个连接窗口,因此可以多人实时共享会话

4. tmux支持窗口任意垂直和水平拆分
```

## 前缀键

tmux窗口有大量的快捷键.所有的快捷键都要通过前缀键唤起.默认的前缀键是"ctrl+b",即按下"ctrl+b",快捷键才会生效

## 会话管理

### 新建会话

第一个启动的,tmux会话窗口,编号是0.第二个窗口的编号是1.

**新建一个指定名称的会话**

```
tmux new -s <session-name>
```

### 分离会话

按下"ctrl+b d"或者输入"tmux detach"命令,就会将当前会话与窗口分离

```
tmux detach
```

执行上面的命令,就会退当前的tmux窗口,但是会话和里面的进程仍然在后台运行

"tmux ls"命令可以查看当前所有的tmux会话

```
tmux ls
or
tmux list-session
```

### 接入会话

"tmux attach"命令用于重新接入某个已经存在的会话

```
# 使用会话编号
tmux attach -t 0

# 使用会话名称
tmux attach -t <session-name>
```

### 杀死会话

"tmux kill-session"命令用于杀死某个会话

```
# 使用会话编号
tmux kill-session -t 0

# 使用会话名称
tmux kill-session -t <session-name>
```

### 切换会话

"tmux switch"命令用于切换会话

```
# 使用会话编号
tmux switch -t 0

# 使用会话名称
tmux switch -t <session-name>
```

### 重命名会话

"tmux rename-session"命令用于重命名会话

```
tmux rename-session -t 0 <new-name>
```

上面命令将0号会话重命名

### 会话快捷键

```
1. ctrl+b+d : 分离当前会话

2. ctrl+b+s : 列出所有会话

3. ctrl+b+$ : 重命名当前会话
```

## 最简操作流程

```
1. 新建会话: tmux new -s <session-name>

2. 在tmux运行所需程序

3. 按下快捷键"ctrl+b+d"将会话分离

4. 下次使用时,重新连接到会话: tmux attach-session -t <session-name>
```

## 窗口操作

tmux可以将窗口分成多个窗格,每个窗格运行不同的命令

### 划分窗格

```
# 划分上下两个窗格
tmux split-window

# 划分左右两个窗格
tmux split-window -h
```

### 移动光标

```
# 光标移动到上窗格
tmux select-pane -U

# 光标移动到下窗格
tmux select-pane -D

# 光标移动到左窗格
tmux select-pane -L

# 光标移动到右窗格
tmux select-pane -R
```

### 交换窗格位置

"tmux swap-pane"命令用于交换窗格的位置

```
# 当前窗格上移
tmux swap-pane -U

# 当前窗格下移
tmux swap-pane -D
```

### 窗格快捷键

```
1. ctrl+b+% : 划分左右两个窗格

2. ctrl+b+" : 划分上下两个窗格

3. ctrl+b+; : 光标移动到上窗格

4. ctrl+b+o : 光标移动到下窗格

5. ctrl+b+x : 关闭当前窗格

6. ctrl+b+! : 将当前窗格拆分为一个独立的窗格

7. ctrl+b+z : 当前窗格全屏显示,再使用一次会变回原来的大小

8. ctrl+b+q : 显示窗格编号
```

## 窗口管理

### 新建窗口

"tmux new-window"命令用来创建新窗口

```
tmux new-window

# 新建一个指定名称的窗口
tmux new-window -n <window-name>
```

### 切换窗口

"tmux select-window"命令用来切换窗口

```
# 切换到指定编号的窗口
tmux select-window -t <window-number>

# 切换到指定名称的窗口
tmux select-window -t <window-name>
```

### 重命名窗口

"tmux rename-window"命令用于为当前窗口起名

```
tmux rename-window <new-name>
```

### 窗口快捷键

```
1. ctrl+b+c : 创建一个新窗口,状态栏会显示多个窗口信息

2. ctrl+b+p : 切换到上一个窗口

3. ctrl+b+n : 切换到下一个窗口

4. ctrl+b+<number> : 切换到指定编号的窗口

5. ctrl+b+w : 从列表中选择窗口

6. ctrl+b+, : 重命名窗口
```

