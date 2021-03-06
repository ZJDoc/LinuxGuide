
# [LOCALE]字符集设置

使用`docker ubuntu`系统时发现无法在`bash`上输入中文，以及中文文件乱码问题，查阅了相关资料，发现是因为字符集的关系

## 查询

使用命令`locale`进行字符集查询

查询当前已缓存字符集

```
$ locale -a
C
C.UTF-8
POSIX
zh_CN.utf8
```

查询当前使用的字符集

```
$ locale
LANG=zh_CN.UTF-8
LANGUAGE=zh_CN.UTF-8
LC_CTYPE="zh_CN.UTF-8"
LC_NUMERIC="zh_CN.UTF-8"
LC_TIME="zh_CN.UTF-8"
LC_COLLATE="zh_CN.UTF-8"
LC_MONETARY="zh_CN.UTF-8"
LC_MESSAGES="zh_CN.UTF-8"
LC_PAPER="zh_CN.UTF-8"
LC_NAME="zh_CN.UTF-8"
LC_ADDRESS="zh_CN.UTF-8"
LC_TELEPHONE="zh_CN.UTF-8"
LC_MEASUREMENT="zh_CN.UTF-8"
LC_IDENTIFICATION="zh_CN.UTF-8"
LC_ALL=zh_CN.UTF-8
```

各个键值函数参考[Locale](https://help.ubuntu.com/community/Locale)

* `LANG`：为未显式设置的`LC_*`变量提供默认值
* `LC_ALL`：重写单个`LC_*`设置：如果设置了`LC_ALL`，则以下任何一项都不会有任何效果

## /etc/default/locale

当前使用的字符集设置保存在文件`/etc/default/locale`中

```
$ cat /etc/default/locale 
#  File generated by update-locale
LANG=zh_CN.UTF-8
LANGUAGE=zh_CN.UTF-8
LC_ALL=zh_CN.UTF-8
```

## 设置zh_CN.UTF-8字符集

首先使用`locale -a`查询本地是否已安装`zh_CN.UTF-8`，如果没有需要下载

```
$ locale-gen zh_CN.UTF-8
```

下载完成后更新配置文件

```
$ update-locale LANG=zh_CN.UTF-8 LANGUAGE=zh_CN.UTF-8 LC_ALL=zh_CN.UTF-8
```

同时设置环境变量

```
# 修改文件/etc/profile
$ sudo vim /etc/profile
...
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN.UTF-8
export LC_ALL=zh_CN.UTF-8
```

重启后即可完成`zh_CN.UTF-8`字符集设置

*对于`en_US.UTF-8`字符集的设置类似*

## 无字符集设置

没有`/etc/default/locale`文件，`locale`查询结果如下：

```
$ locale -a
C
C.UTF-8
POSIX
```

表明当前系统没有区域设置。首先安装配置文件和工具

```
$ sudo apt-get install locales
```

其次使用上面的配置流程进行区域配置

## 相关阅读

* [No locale set](https://www.thomas-krenn.com/en/wiki/Configure_Locales_in_Ubuntu)