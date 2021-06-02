
# [aria2]下载工具

今天在同事的帮助下终于搞定了`Linux`环境下磁力链下载的实现，使用[aria2](http://aria2.github.io/)实现，不需要在去虚拟机中开启迅雷下载了

## 简介

>aria2 is a lightweight multi-protocol & multi-source command-line download utility. It supports HTTP/HTTPS, FTP, SFTP, BitTorrent and Metalink. aria2 can be manipulated via built-in JSON-RPC and XML-RPC interfaces.

## 安装

```
$ sudo apt install aria2
```

## 操作

```
aria2c -x 16 -c 'magnet:?xt=urn:btih:d9027770e6b72966896a4c612cf8ff0e67c7fc28&dn=%e9%98%b3%e5%85%89%e7%94%b5%e5%bd%b1www.ygdy8.com.%e5%90%8c%e5%ad%a6%e9%ba%a6%e5%a8%9c%e4%b8%9d.HD.1080p.%e5%9b%bd%e8%af%ad%e4%b8%ad%e5%ad%97.mkv&tr=udp%3a%2f%2ftracker.opentrackr.org%3a1337%2fannounce&tr=udp%3a%2f%2fexplodie.org%3a6969%2fannounce&tr=udp%3a%2f%2fexodus.desync.com%3a6969%2fannounce'
```

* `-c`：断点续传
* `-x`：分段下载功能

**注意：下载开始后，`aria2`会现在本地创建一个空文件，其大小和最终大小一致**