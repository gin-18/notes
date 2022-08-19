# ranger

## 文件管理器 (ranger)

`ranger`是终端下的文件管理器。

```sh
sudo pacman -S ranger
```

通过以下命令生成`ranger`的配置文件：

```sh
ranger --copy-config=all
```

`ranger`的配置文件在`~/.config/ranger/`目录下。

### ranger 下预览图片

---

安装`ueberzug`可以在`ranger`预览图片。

```sh
sudo pacman -S ueberzug
```

在`~/.config/ranger/rc.conf`文件中找到以下代码：

```sh
# 需要将 false 修改为 ture
set preview_images false     ->     set preview_images ture

# 需要将 w3m 修改为 ueberzug 
set preview_images_method w3m     ->     set preview_images_method ueberzug
```

### ranger 下预览视频

---

安装` ffmpegthumbnailer`可以在`ranger`预览视频

```sh
sudo pacman -S ffmpegthumbnailer
```

在`~/.config/ranger/scope.sh`文件中找到一下代码，并将注释放开。

```sh
## Video
video/*)
    # Thumbnail
    ffmpegthumbnailer -i "${FILE_PATH}" -o "${IMAGE_CACHE_PATH}" -s 0 && exit 6
    exit 1;;
```

### ranger 下预览pdf

---

安装`poppler`可以在`ranger`预览`pdf文件`。

```sh
sudo pacman -S poppler
```

在`~/.config/ranger/scope.sh`文件中找到一下代码，并将注释放开。

```sh
## PDF
application/pdf)
    pdftoppm -f 1 -l 1 \
             -scale-to-x "${DEFAULT_SIZE%x*}" \
             -scale-to-y -1 \
             -singlefile \
             -jpeg -tiffcompression jpeg \
             -- "${FILE_PATH}" "${IMAGE_CACHE_PATH%.*}" \
        && exit 6 || exit 1;;
```

## 安装插件

### Ranger Devicons plugin(file icon glyphs for ranger)

---

依赖：NERDfont 

github地址：https://github.com/ryanoasis/nerd-fonts

**安装**

```
git clone https://github.com/alexanderjeurissen/ranger_devcions ~/.config/ranger/plugins/ranger_devcions

echo "default_linemode devicons >> $HOME/.config/ranger/rc.conf"
```


