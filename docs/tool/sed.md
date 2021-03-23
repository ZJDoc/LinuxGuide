
# [sed]文本替换

>sed is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline). While in some ways similar to an editor which permits scripted edits (such as ed), sed works by making only one pass over the input(s), and is consequently more efficient. But it is sed’s ability to filter text in a pipeline which particularly distinguishes it from other types of editors.

`sed`是一个流编辑器。流编辑器用于对输入流(文件或管道输入)执行基本的文本转换。虽然在某些方面类似于允许脚本编辑的编辑器(如`ed`)，但`sed`只通过一次传递输入来工作，因此效率更高。但是`sed`在管道中过滤文本的能力使它与其他类型的编辑器有着特别的区别

## 定义

```
sed [选项]... {脚本(如果没有其他脚本)} [输入文件]...
```

* `[选项]...`：可包含多个选项
* `{脚本(如果没有其他脚本)}`：替换内容和原内容
* `[输入文件]...`：可包含多个文件

常用的选项有：

* `-i`：在原文件替换内容

### 脚本

常用的脚本有：

* `s/regexp/replacement/flags`：替换内容

其中常用的`flags`有:

* `g`：全局替换

对于斜杆`/`而言，使用反斜杆`\`进行转义，比如原先内容为`http://aaa.com`，那么实现如下：

```
's/http:\/\/aaa.com/replacement/flags'
```

## 示例

测试文件`input.txt`，其内容为

```
hello world

hello zj

hi world

hi zj
```

### 无选项使用

使用`hi`替换`hello`

```
$ sed 's/hello/hi/g' input.txt 
hi world

hi zj

hi world

hi zj
```

**Note：默认操作结果不覆盖原文件**

### 覆盖原文件

```
$ sed -i 's/hello/hi/g' input.txt 
$ cat input.txt 
hi world

hi zj

hi world

hi zj
```

## 相关阅读

* [sed, a stream editor](https://www.gnu.org/software/sed/manual/sed.html)