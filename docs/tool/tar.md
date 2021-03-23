
# [tar]解压缩文件和目录

`tar`是`Linux`系统下的解压缩命令，常用压缩格式为`.tar.gz`

## 参数解析

`tar`常用参数

1. `-z`：通过`gzip`压缩成档案文件
2. `-c`：创建一个新档案文件
3. `-v`：详细地列出处理的文件
4. `-f`：使用档案文件或`ARCHIVE`设备
5. `-x`：从档案文件中解压出文件
6. `-t`：列出归档内容
7. `-C`：改变至目录 `DIR`

## 压缩

压缩指定文件

    $ tar -zcvf file.tar.gz file1 file2 ...

压缩当前目录所有文件

    # 不包括隐藏文件
    $ tar -zcvf file.tar.gz *
    # 包括隐藏文件
    $ tar -zcvf file.tar.gz * .[!.]*

压缩文件夹

    $ tar -zcvf test.tar.gz test
    
## 列出压缩文件内容

    $ tar -tf test.tar.gz

## 解压

### .tar.gz

    # 解压到当前文件夹
    $ tar -zxvf file.tar.gz
    # 解压到指定文件夹，注意：des已存在
    $ tar -zxvf file.tar.gz -C des

### .tar.xz

```
# 解压.xz文件
$ xz -d xxx.tar.xz
# 解压.tar文件
$ tar -xvf xxx.tar
```

## .tar

```
$ tar -xvf xxx.tar
```