
# [WPS]中文字体

## 复制中文字体

在`Windows`操作系统，进入`C:\Windows\Fonts`

```
$ mkdir wps
# 拷贝ttf/TTF/otf/simsun.ttc字体
$ cp *.ttf .\wps\
$ cp *.TTF .\wps\
$ cp *.otf .\wps\
$ cp simsun.ttc .\wps\
```

打包这些字体，传入`Linux`系统

## 配置中文字体

在`Linux`操作系统，进入`/usr/share/fonts/`，新建文件夹`wps_symbol_fonts`，放置中文字体

```
$  chmod 755 wps_symbol_fonts
$ cd wps_symbol_fonts
$ chmod 644 *
$ mkfontscale
$ mkfontdir
$ fc-cache
```

## 相关阅读

* [Linux系统下为WPS添加字体，实现WPS输入中文](https://blog.csdn.net/haolt2010/article/details/52955864)