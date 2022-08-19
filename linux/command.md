# Linux Command

---

[TOC]

## the_silver_searcher

---

ag会默认忽略.gitignore中的文件。

可以创建.ignore文件覆盖.gitignore和.hgignore中忽略的文件。

## tar

---

tar打包，gzip和bzip2压缩。

### 打包压缩

---

gzip方式

```
tar -zcvf <包名(.tar.gz)> <压缩的文件或目录>
```

bzip2方式

```
tar -jcvf <包名(.tar.bz2)> <压缩的文件或目录>
```

### 解压缩

---

gzip方式

```
tar -zxvf <包名> -C <指定目录>
```

bzip2方式

```
tar -jxvf <包名> -C <指定目录>
```

## rar

---

压缩：a

解压缩：x

## xclip

---

复制到剪贴板

```sh
cat <filename> | xclip -selection clipboard

```

## import

---

抓取选区

```
import a.png
```

延时抓取

```
sleep 5;import a.png
```

截取窗口

```
import -frame a.png
```

抓取桌面

```
import -window root a.png
```

## ffmpeg

---

截图

```
# 截取一帧
ffmpeg -ss <start time> -i input -vframes 1 -q:v <1-5> output.png
```

裁剪

```
ffmpeg -ss <start time> -i input.mp4 -t <time num> -c copy output.mp4
```

## convert

---

<++>


















