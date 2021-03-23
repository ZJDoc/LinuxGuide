# [Thinkpad T470p]安装Ubuntu 16.04单系统及Nvidia显卡驱动安装

今天在`Thinkpad T470p`上面重新安装了`Ubuntu16.04`以及`Nvidia`显卡驱动，整个安装过程比之前在其他电脑上安装快很多

不过还是出现了一些问题，记录其中的关键点

## 笔记本查询

参考[thinkpad t470p 安装ubuntu16.04](https://www.jianshu.com/p/013dce15a106)才知道可在`Ubuntu`官网上查询你的笔记本或者台式机是否能够很好的匹配`Ubuntu`，

查询地址：[Ubuntu Desktop certified hardware](https://certification.ubuntu.com/desktop/)

## `Ubuntu16.04`安装

### `U`盘制作

使用软件[Universal USB Installer](https://baike.baidu.com/item/Universal%20USB%20Installer)

### `U`盘安装

先进入`BIOS`设置`U`盘启动优先，进入系统后点击桌面上的安装图标，按照提示进行即可

这里需要注意的是分区问题，选择手动进行分区

首先还原之前已分区的空间，注意：保留`efi`分区（`windows boot manager`）

现在只需要分区`根目录、交换空间和home目录`，不再需要设置`boot`空间，最后还需要将选项`安装启动引导器的设备`设置为`windows boot manager`

## `Nvidia`显卡驱动安装

参考：

[Ubuntu下安装nvidia显卡驱动（安装方式简单）](https://blog.csdn.net/linhai1028/article/details/79445722)

[Linux secure boot(安全启动)时添加Nvidia显卡驱动](http://www.cnblogs.com/dreamyphone/p/4508090.html)

[Ubuntu16.04 安装NVIDIA英伟达驱动教程 及常见几种报错Error的解决方案](https://blog.csdn.net/ksws0292756/article/details/79160742)

[配有 Nvidia 显卡的笔记本安装 ubuntu18.04 所遇到的问题与解决](https://blog.csdn.net/bush_nj/article/details/80850937)

### 下载

查询显卡信息

    $ lspci | grep -i nvidia

    02:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev a2)

在官网上下载相应驱动：[Download Drivers](https://www.nvidia.com/Download/index.aspx)

### 预处理

禁用`Ubuntu`预先安装的`nouveau`驱动

编辑文件`blacklist.conf`，添加屏蔽项

    sudo gedit /etc/modprobe.d/blacklist.conf

    blacklist rivafb
    blacklist vga16fb
    blacklist nouveau
    blacklist nvidiafb
    blacklist rivatv

卸载之前可能存在的`Nvidia`驱动

    # 如果存在
    nvidia-uninstall

    sudo apt-get --purge remove nvidia-*
    sudo apt-get autoremove

给驱动设置权限

    sudo chmod a+x NVIDIA-Linux*.run

### 安装驱动

关闭窗口桌面

    sudo service lightdm stop

切换到命令行桌面`Ctrl+Alt+F1`，执行驱动更新

    sudo ./NVIDIA-Linux-x86_64-410.93.run -no-x-check -no-nouveau-check -no-opengl-files

驱动会显示如下问题

**问题一：the distribution-provided pre-install script failed!**

继续执行

**问题二：`dkms`**

选择no

**问题二：`sign the kernel module`**

需要签名才能写入，选择签名，并且重新生成，不删除私钥

安装完成后将密钥写入内核信任列表

    sudo mokutil --import /usr/share/nvidia/nvidia*.der

会要求输入两次密码（自定义），然后重启应用

    sudo reboot

**问题三：`perform mok management`**

重启后会进入一个蓝色界面，需要你手动写入签名

1. 选择`enroll mok `
2. 选择`continue`
3. 选择 `yes` 
4. 输入之前设置的密码
5. 选择`reboot`

这样驱动就成功安装了

    zj@zj-ThinkPad-T470p:~$ nvidia-smi 
    Fri Jan 11 20:57:56 2019       
    +-----------------------------------------------------------------------------+
    | NVIDIA-SMI 410.93       Driver Version: 410.93       CUDA Version: 10.0     |
    |-------------------------------+----------------------+----------------------+
    | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    |===============================+======================+======================|
    |   0  GeForce 940MX       Off  | 00000000:02:00.0 Off |                  N/A |
    | N/A   33C    P0    N/A /  N/A |      0MiB /  2004MiB |      1%      Default |
    +-------------------------------+----------------------+----------------------+
                                                                                
    +-----------------------------------------------------------------------------+
    | Processes:                                                       GPU Memory |
    |  GPU       PID   Type   Process name                             Usage      |
    |=============================================================================|
    |  No running processes found                                                 |
    +-----------------------------------------------------------------------------+
