# Linux Command

## pacman

更新软件包数据库，不更新任何软件

```
sudo pacman -Sy
```

升级所有的程序

```
sudo pacman -Syyu
```

从缓存中删除所有的软件包

```
sudo pacman -Sc
```

搜索软件包

```
sudo pacman -Ss <软件包名称>
```

卸载软件包

```
sudo pacman -Rns <软件包名称>
```

列出已安装的软件包

```
sudo pacman -Qe
```

列出从main repository中安装的软件包

```
sudo pacman -Qn
```

列出从AUR中安装的软件包

```
sudo pacman -Qm
```

列出已经不再需要依赖的软件包

```
sudo pacman -Qdt
```

## the_silver_searcher

ag会默认忽略.gitignore中的文件。

可以创建.ignore文件覆盖.gitignore和.hgignore中忽略的文件。

## convert

<++>

















