
# [Ubuntu 16.04]VMware安装

在`Ubuntu`上安装`vmware`后遇到了一些问题，总结一下

## `VMWare WorkStation Pro`下载

官网下载地址：[Try VMware Workstation Pro](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)

## 安装

下载完成后得到一个`.bundle`文件

    VMware-Workstation-Full-15.0.2-10952284.x86_64.bundle

赋予用户权限

    sudo chmod a+x VMware*.bundle

安装

    sudo ./VMware*.bundle

## 问题：`could not open /dev/vmmon...`

新建一个虚拟机后，设置`win10 ISO`文件，开始安装，遇到如下问题

    could not open /dev/vmmon...

有两种解决方案

方案一是直接在`BIOS`中关闭安全启动(`secure boot)`选项

方案二参考

[VMWare 15 Error on Ubuntu 18.4 - Could not open /dev/vmmon: No such file or directory](https://askubuntu.com/questions/1096052/vmware-15-error-on-ubuntu-18-4-could-not-open-dev-vmmon-no-such-file-or-dire)

[VMware Workstation 12 vmmon not found or not loaded](https://askubuntu.com/questions/707281/vmware-workstation-12-vmmon-not-found-or-not-loaded)

其原理是安全启动模式下`vmware`的一些核心模块没有被写入，需要设置信任列表

第一步：生产`.priv`和`.der`文件

    openssl req -new -x509 -newkey rsa:2048 -keyout zj-vmware.priv -outform DER -out zj-vmware.der -nodes -days 36500 -subj "/CN=VMWARE/"

第二步：

    sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./zj-vmware.priv ./zj-vmware.der $(modinfo -n vmmon)
    sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./zj-vmware.priv ./zj-vmware.der $(modinfo -n vmnet)

第三步：

    sudo mokutil --import zj-vmware.der
    # 然后输入两次密码（自定义）

重启之后会进入蓝色界面，需要你手动写入签名

1. 选择`enroll mok `
2. 选择`continue`
3. 选择 `yes` 
4. 输入之前设置的密码
5. 选择`reboot`

测试你是否写入签名

    zj@zj-ThinkPad-T470p:~/software/vmware/mok$ mokutil --test-key zj-vmware.der
    zj-vmware.der is already enrolled

## `Win10`安装

`win10`官网下载地址：[win10 ISO](https://www.microsoft.com/zh-cn/software-download/windows10ISO/)

`win10`注册码：[用真正的序列号永久激活win10教程](http://www.xitongcheng.com/jiaocheng/win10_article_45002.html)

`win10`安装完成后再安装`vmware tools`

    打开vmware菜单栏->VM->Install VMware Tools

没有自动适配屏幕就参考[VMware问题 ,我装了WIN10也装了VMTools,依然没法自动适应窗口?](http://ask.zol.com.cn/x/3585482.html)

    打开vmware菜单栏->edit->Preferences->Display，点击Autofit guest