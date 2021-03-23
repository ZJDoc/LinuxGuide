
# [tee]数据写入和输出

`tee`命令用于读取标准输入（`stdin`）的数据，同时写入文件和输出到标准输出（`stdout`）

## 语法

```
tee [OPTION]... [FILE]...
```

* 默认将输入数据覆盖写入指定文件
* 可以同时写入到多个文件
* 使用参数`-a`表示以追加方式写入文件

通过管道方式将标准输入数据传输到`tee`，比如

```
$ cat tt.txt | tee a.txt
```

## 示例

写入单个文件

```
$ echo "hello world" | tee hello.txt
hello world
$ cat hello.txt 
hello world
```

写入多个文件

```
$ echo "hello world" | tee hello.txt hello2.txt
```

以追加方式写入

```
$ echo "hello world" | tee -a hello.txt hello2.txt
```

如果只想要写入文件而不输出到`stdout`，需要重定向到`/dev/null`

```
$ echo "hello world" | tee hello.txt >> /dev/null
```

## 相关阅读

* [Linux tee命令](https://www.runoob.com/linux/linux-comm-tee.html)