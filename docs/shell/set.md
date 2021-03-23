
# set

`set`命令可以辅助脚本运行

## 环境变量

在命令行直接输入`set`，将输出所有的环境变量和`shell`函数

## set -eux

* `-e`：若命令返回值不等于`0`，则立即退出
* `-u`：执行时使用到未定义过的变量时，显示错误信息并停止运行
* `-x`：先输出命令，再输出其运行结果

`set -e`不适用于管道命令

>管道命令指的是多个子命令通过管道运算符（|）组合成为一个大的命令。Bash会把最后一个子命令的返回值，作为整个命令的返回值。也就是说，只要最后一个子命令不失败，管道命令总是会执行成功，因此它后面命令依然会执行，set -e就失效了

可通过`set -o pipefail`解决此问题，`-o pipefail`的作用是一个子命令失败，整个管道命令就失败

## 小结

在每次`shell`脚本的开头加入以下`set`语句

```
set -eux
set -o pipefail
```

有助于脚本的调试和实现

对于无法编辑的脚本，可通过命令行传入`set`命令

```
$ bash -euxo pipfail script.sh
```

## 相关阅读

* [Linux set命令](https://www.runoob.com/linux/linux-comm-set.html)

* [Bash 脚本 set 命令教程](http://www.ruanyifeng.com/blog/2017/11/bash-set.html?utm_source=tool.lu)
