
# [cp]复制目录下排除某个文件或文件夹外的所有文件

假设源目录地址为`dir-A`，结果目标地址为`dir-B`，要求是复制`dir-A`下所有文件/文件夹到`dir-B`，除了文件/文件夹`ccc`

1. 进入源目录地址
2. 执行复制命令

```
$ cd dir-A
$ cp -r `ls dir-A | grep -v ccc | xargs` dir-B
```

## 相关阅读

* [Linux复制目录下排除某个文件或文件夹外的所有文件](https://blog.csdn.net/weixin_42970378/article/details/89177318)