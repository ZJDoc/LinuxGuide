
# [alias]命令别名设置

`alias`是系统自带的命令别名设置工具

## 定义

```
# 定义新的命令别名
alias 新的命令='原命令 选项 参数'
# 取消命令别名
unalias 新的命令
```

## 预定义

`alias`预先定义了几个命令别名

```
$ alias
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
```

## 自定义

临时定义：打开命令行窗口，输入

```
alias ...
```

永久定义，修改`~/.bashrc`，输入

```
alias ...
```

## 相关阅读

* [alias command in Linux with Examples](https://www.geeksforgeeks.org/alias-command-in-linux-with-examples/)

* [alias命令](https://man.linuxde.net/alias)
