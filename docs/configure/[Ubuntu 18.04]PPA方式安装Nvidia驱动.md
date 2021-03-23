
# [Ubuntu 18.04]PPA方式安装Nvidia驱动

参考：

[Ubuntu18.04安装Nvidia显卡驱动教程](https://blog.csdn.net/weixin_43820996/article/details/100676292)

[Ubuntu 18.04安装NVIDIA显卡驱动教程](https://www.linuxidc.com/Linux/2019-02/157170.htm)

之前都是通过手动方式安装`Nvidia`驱动，这一次尝试`PPA`方式安装，操作更加简单

## 禁用nouveau

安装`Nvidia`驱动之前需要禁用`nouveau`

```
$ sudo vim /etc/modprobe.d/blacklist-nouveau.conf
```

添加以下两条语句

```
blacklist nouveau
options nouveau modeset=0
```

更新内核并重启

```
$ sudo update-initramfs -u
$ sudo reboot
```

可以查询是否已禁用

```
$ lspci | grep nouveau
```

## 安装Nvidia驱动

添加`PPA`源

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
```

查询当前适用版本

```
$ ubuntu-drivers devices

== /sys/devices/pci0000:00/0000:00:01.2/0000:02:00.0 ==
modalias : pci:v000010DEd0000134Dsv000017AAsd0000505Ebc03sc02i00
vendor   : NVIDIA Corporation
model    : GM108M [GeForce 940MX]
driver   : nvidia-driver-410 - third-party free
driver   : nvidia-driver-415 - third-party free
driver   : nvidia-driver-430 - distro non-free
driver   : nvidia-driver-435 - distro non-free
driver   : nvidia-driver-390 - third-party free
driver   : nvidia-driver-440 - third-party free recommended
driver   : xserver-xorg-video-nouveau - distro free builtin
```

当前适用`440`版本（通过官网[drivers](https://www.geforce.cn/drivers)查询可知该版本是最新版本），自动安装

```
$ sudo ubuntu-drivers autoinstall
```

安装完成后重启，即完成`Nvidia`驱动安装

```
$ sudo reboot
$ nvidia-smi 
Tue Dec  3 12:58:08 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 440.26       Driver Version: 440.26       CUDA Version: 10.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce 940MX       Off  | 00000000:02:00.0 Off |                  N/A |
| N/A   41C    P0    N/A /  N/A |    385MiB /  2004MiB |      6%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1165      G   /usr/lib/xorg/Xorg                            24MiB |
|    0      1629      G   /usr/bin/gnome-shell                          46MiB |
|    0      1893      G   /usr/lib/xorg/Xorg                           156MiB |
|    0      2085      G   /usr/bin/gnome-shell                         121MiB |
|    0      2963      G   /usr/lib/firefox/firefox                       0MiB |
|    0      3663      G   ...uest-channel-token=10978559456542000038    29MiB |
+-----------------------------------------------------------------------------+
```

*已同时安装了`cuda`*
