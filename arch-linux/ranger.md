# ranger

## ranger的配置文件

安装完成ranger之后，并没有ranger的配置文件，需要执行ranger --copy-config=all

ranger的配置文件在~/.config/ranger目录下

## 安装插件

### Ranger Devicons plugin(file icon glyphs for ranger)

依赖：NERDfont 

github地址：https://github.com/ryanoasis/nerd-fonts

**安装**

```
git clone https://github.com/alexanderjeurissen/ranger_devcions ~/.config/ranger/plugins/ranger_devcions

echo "default_linemode devicons >> $HOME/.config/ranger/rc.conf"
```


