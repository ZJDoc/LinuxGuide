
# [rsync]断点续传

之前经常使用`scp`进行远程文件的传送，不过当传送大文件时，经常下载到一半多后就断掉了。在网上找到一个新的传送工具 - [Rsync](https://wiki.archlinux.org/index.php/Rsync)

## 使用

```
$ rsync -P source destination
```

* `-P`是两个参数的集合 - `--partial --progress`
* `--partial`：保留部分传输的文件，也就是实现断点续传功能
* `--progress`：显示进度

*默认使用`SSH`协议进行传输*

## 相关阅读

* [As cp/mv alternative](https://wiki.archlinux.org/index.php/Rsync)