
# [split][cat]分块或合并大文件

## 分块大文件

使用`split`命令，可以指定字节数

```
split [-b <字节>] [要切割的文件] [输出文件名，也可以是目录]
```

比如按`100MB`分割文件`DJI_0004.MOV`，输出到目录`DJIs`，同时指定文件前缀为`DJI`

```
$ split -b 100MB DJI_0004.MOV DJIs/DJI
$ ls -al DJIs/
总用量 668976
drwxr-xr-x  2 zj zj      4096 3月   3 10:03 .
drwxr-xr-x 16 zj zj      4096 3月   3 10:03 ..
-rw-r--r--  1 zj zj 100000000 3月   3 10:03 DJIaa
-rw-r--r--  1 zj zj 100000000 3月   3 10:03 DJIab
-rw-r--r--  1 zj zj 100000000 3月   3 10:03 DJIac
-rw-r--r--  1 zj zj 100000000 3月   3 10:03 DJIad
-rw-r--r--  1 zj zj 100000000 3月   3 10:03 DJIae
-rw-r--r--  1 zj zj 100000000 3月   3 10:03 DJIaf
-rw-r--r--  1 zj zj  84999932 3月   3 10:03 DJIag
$ du -sh DJIs/
654M	DJIs/
(base) zj@zj-ThinkPad-T470p:~/work$ du -sh DJIs/*
96M	DJIs/DJIaa
96M	DJIs/DJIab
96M	DJIs/DJIac
96M	DJIs/DJIad
96M	DJIs/DJIae
96M	DJIs/DJIaf
82M	DJIs/DJIag
```

## 合并文件

使用`cat`命令将分块文件合并回大文件

```
$ cat DJIs/* > DJI_2.MOV
```

## 参考

* [Linux split命令](https://www.runoob.com/linux/linux-comm-split.html)
* [linux split 命令 大文件 文件分块 文件分割](https://blog.csdn.net/whatday/article/details/105886325)
* [Linux cat 命令](https://www.runoob.com/linux/linux-comm-cat.html)
* [Linux之cat合并多个文件](https://www.cnblogs.com/mrdoghead/p/12010452.html)