## Shell

#### 查看当前运行的 Shell 和 版本号

```bash
$ echo $SHELL
$ bash --version
```

`$`是命令提示符，使用`echo $PS1`可以打印命令提示符的定义。Bash 允许用户自定义命令提示符，只要改写环境变量`PS1`即可，命令提示符可以包含特殊的转义字符，表示特定内容。

 `PS2`保存着命令行折行输入时系统的提示符，默认为`>`。

 `PS3`保存着使用select命令时，系统输入菜单的提示符。

命令提示符默认是显示终端预定义的颜色。Bash 允许自定义提示符颜色。表示颜色的代码，如\033[1;30m：深灰色。除了设置前景颜色，Bash 还允许设置背景颜色。



#### 运行脚本

编辑脚本（文件名 myfirst）：写上`#!/bin/bash` （Shebang 行）的脚本可以直接调用执行。

```bash
#!/bin/bash
echo "Hello World"
```

设置文件执行权限和路径：脚本的权限通常设为755（拥有者有所有权限，其他人有读和执行权限）或者700（只有拥有者可以执行）。除了执行权限，脚本调用时，一般需要指定脚本的路径。建议在主目录新建一个`~/bin`子目录，专门存放可执行脚本，然后把`~/bin`加入`$PATH`。（`export PATH=$PATH:~/bin`）。

```bash
$ chmod +x myfirst
$ ./intro
```

- `chmod +x script.sh`（脚本文件名）：给所有用户执行权限。
- `chmod +rx script.sh`（脚本文件名）：给所有用户读权限和执行权限。此处+rx 可以换成 755.
- `chmod u+rx script.sh`：只给脚本拥有者读权限和执行权限。



#### 打印 ASCII 码

```bash
$ man ascii
```



#### 使用 Homebrew 安装 tree

```bash
$ brew install tree
$ tree demo
```

