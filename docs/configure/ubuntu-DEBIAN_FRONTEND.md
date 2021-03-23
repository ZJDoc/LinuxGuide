
# [Ubuntu]DEBIAN_FRONTEND

环境变量`DEBIAN_FRONTEND`控制安装程序时用户交互界面的类型

共`4`个类型：

1. `noninteractive`
2. `text`
3. `newt`
4. `gtk`

默认`DEBIAN_FRONTEND=newt`

## noninteractive

将`DEBIAN_FRONTEND`设置为`noninteractive`，表示安装软件时不进行交互，选择默认选项进行构建

```
sudo DEBIAN_FRONTEND=noninteractive apt-get -y install [packagename]
```

## 相关阅读

* [DEBIAN_FRONTEND](https://www.debian.org/releases/buster/s390x/ch05s02.en.html)
* [ubuntu DEBIAN_FRONTEND环境变量用法](https://www.cnblogs.com/bollen/p/7137200.html)
* [关于DEBIAN_FRONTEND noninteractive的正确用法](https://wp.goodmemory.cc/%E5%85%B3%E4%BA%8Edebian_frontend-noninteractive%E7%9A%84%E6%AD%A3%E7%A1%AE%E7%94%A8%E6%B3%95/)
* [Ubuntu使用apt-get安装软件禁用交互模式](https://www.centos.bz/2017/12/ubuntu%e4%bd%bf%e7%94%a8apt-get%e5%ae%89%e8%a3%85%e8%bd%af%e4%bb%b6%e7%a6%81%e7%94%a8%e4%ba%a4%e4%ba%92%e6%a8%a1%e5%bc%8f/)
