
# [7zip]解压缩文件和目录

## 安装


* `linux`

```
$ sudo apt-get install p7zip-full
```

* `windows`：[7zip](https://www.7-zip.org/)

## 使用

```
Usage: 7z <command> [<switches>...] <archive_name> [<file_names>...]
       [<@listfiles...>]

<Commands>
  a : Add files to archive
  b : Benchmark
  d : Delete files from archive
  e : Extract files from archive (without using directory names)
  h : Calculate hash values for files
  i : Show information about supported formats
  l : List contents of archive
  rn : Rename files in archive
  t : Test integrity of archive
  u : Update files to archive
  x : eXtract files with full paths
```

* 打包文件/文件夹

```
$ 7z a Sample.zip Sample
```

* 解压文件/文件夹

```
$ 7z e Sample.zip
```