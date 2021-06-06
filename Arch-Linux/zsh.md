# zsh

## zinit

zinit是一个灵活而快速的Zshell插件管理器。zinit

### 安装zinit

克隆仓库到~/.zinit/bin：

```
mkdir ~/.zinit

git clone https://github.com/zdharma/zinit.git ~/.zinit/bin
```

在zshrc文件中source zinit：

```
source ~/.zinit/bin/zinit.zsh
```

## 插件

```
zinit light zsh-users/zsh-autosuggestions

zinit light zdharma/fast-syntax-highlighting

zinit load zdharma/history-search-multi-word
```
