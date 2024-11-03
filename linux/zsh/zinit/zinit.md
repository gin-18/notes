# zsh & 插件管理器 (zinit)

## zsh

```sh
# 安装 zsh
sudo pacman -S zsh

# 切换到 zsh
chsh -s /bin/zsh
```

`zsh`的配置文件为：`~/.zshrc`。

推荐创建`~/.config/zsh/zshrc`文件，并在`～/.zshrc`文件中`source`一下`~/.config/zsh/zshrc`文件。以方便在`~/.config/zsh`目录下配置`zsh`。

```sh
# 修改 ~/.zshrc
vim ~/.zshrc

# 在 .zshrc 中添加以下代码
source ~/.config/zsh/zshrc
```

## 插件管理器 (zinit)

`zinit` 的 `github` 地址：[zinit](https://github.com/zdharma/zinit)

```sh
# 创建 .zinit目录
mkdir ~/.zinit

# 克隆 zinit 仓库
git clone https://github.com/zdharma/zinit.git ~/.zinit/bin

# 在 ～/.config/zsh/zshrc 文件中 source ~/.zinit/bin/zinit.zsh
source ~/.zinit/bin/zinit.zsh
```
