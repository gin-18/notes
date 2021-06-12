# pacman

更新软件包数据库，不更新任何软件

```sh
sudo pacman -Sy
```

更新所有的软件包

```sh
sudo pacman -Syyu
```

从缓存中删除所有的软件包

```sh
sudo pacman -Sc
```

搜索软件包

```sh
sudo pacman -Ss <软件包名称>
```

卸载软件包

```sh
sudo pacman -Rns <软件包名称>
```

列出已安装的软件包

```sh
sudo pacman -Qe
```

列出从main repository中安装的软件包

```sh
sudo pacman -Qn
```

列出从AUR中安装的软件包

```sh
sudo pacman -Qm
```

列出已经不再需要依赖的软件包

```sh
sudo pacman -Qdt
```

在`/etc/pacman.conf`文件中，找到以下代码，将`Color`字段的注释放开并添加`ILoveCandy`。

效果为`pacman`的输出信息拥有颜色，并且进度条为`吃豆人`的样式。

![pacman](./images/pacman.png)
