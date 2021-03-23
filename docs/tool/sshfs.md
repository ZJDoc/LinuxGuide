
# [sshfs]挂载远程文件系统

`sshfs`是一个连接到`SSH`服务器的的远程文件系统客户端，它利用`SFTP`将远程文件系统挂载到本地

## 安装

```
$ sudo apt-get install sshfs
```

## 挂载

通用范式如下：

```
sshfs [user@]host:[dir] mountpoint [options]
```

* 参数`user`指定远程用户名，如果被忽略将使用本地用户名
* 参数`dir`指定远程目录，如果被忽略将挂载远程`home`目录
* 参数`mountpoint`指定本地挂载点

## 卸载

有两种方式

```
$ fusermount -u mountpoint
# 或者
$ umount mountpoint
```

## 相关阅读

* [libfuse/sshfs](https://github.com/libfuse/sshfs)