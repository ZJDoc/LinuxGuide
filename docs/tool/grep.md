
# [grep]文本搜索

## 定义

```
grep [选项]... PATTERN [FILE]...
```

* `[选项]...`：可包含多个选项
* `PATTERN`：匹配字符串
* `[FILE]...`：可搜索多个文件

常用的选项有：

1. `-i`：忽略大小写
2. `-r`：递归搜索
3. `-l`：输出**符合**`PATTERN`的文件名
4. `-L`：输出**不包含**`PATTERN`的文件名
5. `-n`：输出符合`PATTERN`的行数

## 示例

**Note：可组合多个选项一起使用**

### 无选项使用

```
$ grep "内容" examples.desktop 
Comment[zh_CN]=Ubuntu 示例内容
```

### 打印行数

```
$ grep -n "内容" examples.desktop 
234:Comment[zh_CN]=Ubuntu 示例内容
```

### 忽略大小写

```
$ grep -i icon examples.desktop 
Icon=folder
```

### 递归搜索

```
~/nginx$ grep -r access .
./conf.d/default.conf:    #access_log  /var/log/nginx/host.access.log  main;
./conf.d/default.conf:    # deny access to .htaccess files, if Apache's document root
./nginx.conf:    access_log  /var/log/nginx/access.log  main;
```

### 打印符合条件的文件名

配置递归选项一起操作

```
$ grep -rl access .
./conf.d/default.conf
./nginx.conf
```

## 相关阅读

* [Linux 查找文本工具grep](https://blog.csdn.net/u012005313/article/details/46389441)