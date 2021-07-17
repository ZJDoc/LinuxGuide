
# tmux

[tmux](https://github.com/tmux/tmux)是类似于[screen](https://www.runoob.com/linux/linux-comm-screen.html)命令的终端复用器（`terminal multiplexer`）

## 介绍

>1.1 会话与进程
>
>命令行的典型使用方式是，打开一个终端窗口（terminal window，以下简称"窗口"），在里面输入命令。用户与计算机的这种临时的交互，称为一次"会话"（session） 。
>
>会话的一个重要特点是，窗口与其中启动的进程是连在一起的。打开窗口，会话开始；关闭窗口，会话结束，会话内部的进程也会随之终止，不管有没有运行完。
>
>一个典型的例子就是，SSH 登录远程计算机，打开一个远程窗口执行命令。这时，网络突然断线，再次登录的时候，是找不回上一次执行的命令的。因为上一次 SSH 会话已经终止了，里面的进程也随之消失了。
>
>为了解决这个问题，会话与窗口可以"解绑"：窗口关闭时，会话并不终止，而是继续运行，等到以后需要的时候，再让会话"绑定"其他窗口。
>
>1.2 Tmux 的作用
>
>Tmux 就是会话与窗口的"解绑"工具，将它们彻底分离。

## 安装

```
sudo apt install tmux
```

## 使用

* 新建会话

打开一个窗口，输入

```
# 默认
$ tmux
# 设置会话名
$ tmux new -s <session-name>
```

* 分离会话

使用快捷键`Ctrl+b d`

* 查询会话

```
$ tmux ls
0: 1 windows (created Wed Jun  2 19:31:03 2021) [80x23]
abc: 1 windows (created Wed Jun  2 19:43:01 2021) [80x23]
```

默认会话从`0`开始编号，如果显式设置会话名，则会显示会话名

* 进入会话

```
$ tmux a<或者attach> -t <会话名>
```

* 杀死会话

先进入会话，然后显式结束该窗口（输入`exit`）即可杀死该会话；或者输入如下命令

```
$ tmux kill-session -t <会话名>
```

* 鼠标可滚动

先执行命令`ctrl+b`，然后输入

```
set -g mouse on
```

## 相关阅读

* [Tmux 使用教程](http://www.ruanyifeng.com/blog/2019/10/tmux.html)
* [如何使tmux能够使用鼠标上下滚动？](https://www.cnblogs.com/dakewei/p/14185174.html)