
# [zip]解压缩文件和目录

`zip`是跨平台(`Windows/Linux`)的解压缩命令，压缩格式为`.zip`

## 参数解析

`zip`常用参数：

1. `-r`：递归目录

`unzip`常用参数

1. `-d`：解压到指定目录

## 压缩

压缩指定文件

    $ zip test.zip file1 file2 ...

压缩当前目录所有文件

    # 不包括隐藏文件
    $ zip test.zip *
    # 包括隐藏文件
    $ zip test.zip * .[!.]*

压缩文件夹

    $ zip -r test.zip te3
    
## 解压

    # 解压到当前文件夹
    $ unzip test.zip
    # 解压到指定文件夹，如果不存在则新建
    $ unzip test.zip -d des
