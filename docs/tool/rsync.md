
# [rsync]传输

## 断点续传

之前经常使用`scp`进行远程文件的传送，不过当传送大文件时，经常下载到一半多后就断掉了。在网上找到一个新的传送工具 - [Rsync](https://wiki.archlinux.org/index.php/Rsync)

```
$ rsync -P source destination
```

* `-P`是两个参数的集合 - `--partial --progress`
* `--partial`：保留部分传输的文件，也就是实现断点续传功能
* `--progress`：显示进度

*默认使用`SSH`协议进行传输*

## 文件同步

文件传输的另一种理解就是文件同步了，对于文件/文件夹的同步，`rsync`非常有效

```
# 同步本地文件夹到远程
$ rsync -av local_folder/   <username>@<remote_ip>:/path/to/remote_folder
# 同步远程到本地
$ rsync -av <username>@<remote_ip>:/path/to/remote_folder/   local_folder
# 同步到远程的过程中删除在远程目录中本地不存在的文件
$ rsync -av --delete <username>@<remote_ip>:/path/to/remote_folder/   local_folder
```

* `-a`：打包方式，等同于`-rlptgoD (no -H,-A,-X)`
* `-v`：输出传输信息

**注意：`/`很重要**

## Rsync chown/chgrp出错

* 参考：[解决 Rsync chown/chgrp 错误](https://blog.csdn.net/weixin_34327223/article/details/93397587)

## 相关阅读

* [As cp/mv alternative](https://wiki.archlinux.org/index.php/Rsync)
* [rsync](https://en.wikipedia.org/wiki/Rsync)