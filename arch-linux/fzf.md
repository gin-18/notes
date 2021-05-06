# fzf

官方github：https://github.com/junegunn/fzf

## fzf安装、更新和卸载

#### 安装fzf

```
1. 脚本安装：git clone https://github.com/junegunn/fzf.git ~/.fzf --depth 1

~/.fzf/install

2. 也可以使用包管理工具进行安装
```

#### 更新

```
cd ~/.fzf && git pull && ./install
```

#### 卸载

```
cd ~/.fzf/uninstall
```

## 搜索工具(the_silver_searcher)

```
sudo pacman -S the_silver_searcher
```

## fzf预览窗口

预览窗口高亮需要安装bat

```
sudo pacman -S bat
```

#### 修改bat样式

在zshrc文件中添加以下代码：

```
export BAT_STYLE="changes"
```

## 命令补全

```
vim \<Tab>

cd \<Tab>

kill -9 <Tab>

ssh \<Tab>

telnet \<Tab>

unset \<Tab>

export \<Tab>

unalias \<Tab>
```

## fzf.vim

使用回车键在当前窗口打开选中的文件

使用ctrl-t在新的标签页打开选中的文件

使用ctrl-x以上下分屏的方式打开选中的文件

使用ctrl-v是 以左右分屏的方式打开选中的文件

## ranger的fzf脚本

```python
class fzf_select(Command):
    """
    :fzf_select
    Find a file using fzf.
    With a prefix argument select only directories.
    See: https://github.com/junegunn/fzf
    """
    def execute(self):
        import subprocess
        import os.path
        if self.quantifier:
            # match only directories
            command = "find -L . \( -path '*/\.*' -o -fstype 'dev' -o -fstype 'proc' \) -prune \
            -o -type d -print 2> /dev/null | sed 1d | cut -b3- | fzf +m"

        else:
            # match files and directories
            command = "find -L . \( -path '*/\.*' -o -fstype 'dev' -o -fstype 'proc' \) -prune \
            -o -print 2> /dev/null | sed 1d | cut -b3- | fzf +m"

        fzf = self.fm.execute_command(command,
                                      universal_newlines=True,
                                      stdout=subprocess.PIPE)
        stdout, stderr = fzf.communicate()
        if fzf.returncode == 0:
            fzf_file = os.path.abspath(stdout.rstrip('\n'))
            if os.path.isdir(fzf_file):
                self.fm.cd(fzf_file)
            else:
                self.fm.select_file(fzf_file)
```


