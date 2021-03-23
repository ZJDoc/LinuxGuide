
# [Ubuntu 18.04]VMware安装

参考：[在ubuntu18.04上安装vmware](https://blog.csdn.net/qq_43658650/article/details/86663326)

在`Ubuntu 18.04`上安装`VMware`，之前虽然在`16.04`上安装过（[[Ubuntu 16.04]VMware安装](./[Ubuntu 16.04]VMware安装.md)），但是这次操作发现还有一些需要调整的地方

## 下载

一定要去官网下载最新版本：[Try VMware Workstation Pro](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)

当前使用：

```
$ vmware-installer -l
Product Name         Product Version     
==================== ====================
vmware-workstation   15.5.1.15018445     
```

## 必备条件

安装以下应用：

```
$ sudo apt install gcc g++ libcanberra-gtk-module build-essential
```

## 安装

首先赋予执行权限

```
$ sudo chmod a+x VMware-Workstation-Full-15.5.1-15018445.x86_64.bundle
```

然后进行安装

```
$ sudo ./VMware-Workstation-Full-15.5.1-15018445.x86_64.bundle
Extracting VMware Installer...done.
Installing VMware Installer 3.0.0
...
...
Installing VMware Workstation 15.5.1
Copying files...
Configuring...
Installation was successful.
```

安装完成后启动`VMware`，进入图形界面进行配置即可

## 卸载

参考：[有关于ubuntu16.04 卸载vmware](https://blog.csdn.net/smile_5me/article/details/80799328)

```
$ sudo vmware-installer --uninstall-product vmware-workstation
```

## 服务设置

安装完`VMWare`之后，默认开启了`3`个服务

```
vmware.service                     vmware-workstation-server.service
vmware-USBArbitrator.service 
```

禁止`VMWare`相关服务自启动

```
# 禁止开机自启动
$ sudo systemctl disable xxx
# 停止服务
$ sudo systemctl stop xxx
```

## could not open /dev/vmmon:????????

打开`vmware`时会出现`could not open /dev/vmmon:????????.`错误

* 解决一：参考[关于ubuntu安装VMware出现“could not open /dev/vmmon:????????.”的解决方法-已解决](https://blog.csdn.net/weixin_40894428/article/details/84843199)
* 解决二：查看是否`vmware`相关的`service`是否被关闭了，重新启动即可解决