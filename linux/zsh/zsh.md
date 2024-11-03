# Zsh

Zsh官方地址：[Zsh](https://www.zsh.org/)

## Arch Linux 安装 zsh

```sh
sudo pacman -S zsh
```

## 切换到 zsh

```sh
chsh -s /bin/zsh
```

## 统一管理 zsh 配置

`zsh` 默认配置文件是 `~/.zshrc`。

可以创建 `~/dotfiles/zsh` 目录，将所有有关 `zsh` 的配置都放在这个目录里。

```sh
# 创建目录并进入
mkdir -p ~/dotfiles/zsh && cd ~/dotfiles/zsh

# 创建 zshrc 文件用于代替 .zshrc
touch zshrc
```

在 `~/.zshrc` 文件中添加以下内容：

```sh
echo "source ~/dotfiles/zsh/zshrc" > ~/dotfiles/zsh/zshrc
```

这样就可以使用 `~/dotfiles/zsh/zshrc` 来配置 `zsh` 了。

## 插件

### 插件管理器 - zinit

插件管理器地址：[zdharma-continuum/zinit](https://github.com/zdharma-continuum/zinit)

### 安装 zinit

<++>

### 推荐插件

```
zinit light zsh-users/zsh-autosuggestions

zinit light zdharma/fast-syntax-highlighting

zinit load zdharma/history-search-multi-word
```
