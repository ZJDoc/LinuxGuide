
# ERROR

## 问题一：Network service discovery disabled

经常会遇到一个问题：在开机或者切换网络过程中，右上角弹出一个提示框，显示

```
Network service discovery disabled
```

参考[Network service discovery disabled: What does this mean for me?](https://askubuntu.com/questions/339702/network-service-discovery-disabled-what-does-this-mean-for-me)

进入目录`/etc/default/`，修改文件`avahi-daemon`如下：

```
# 1 = Try to detect unicast dns servers that serve .local and disable avahi in
# that case, 0 = Don't try to detect .local unicast dns servers, can cause
# troubles on misconfigured networks
# AVAHI_DAEMON_DETECT_LOCAL=1
AVAHI_DAEMON_DETECT_LOCAL=0
```

重启即可

## 问题二：[VIM]中文乱码

参考：[解决配置vim中文乱码的问题](https://blog.csdn.net/weixin_36250487/article/details/79888103)

`vim`配置文件为`vimrc`

    $ cd /etc/vim
    $ cat vimrc
    ...
    ...
    " Source a global configuration file if available
    if filereadable("/etc/vim/vimrc.local")
    source /etc/vim/vimrc.local
    endif

新建文件`vimrc.local`，添加如下语句

    set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
    set termencoding=utf-8
    set encoding=utf-8

## 问题三：[SHELL]命令行窗口假死

参考：[linux命令行模式下输入Ctrl+s后界面锁定，假死](https://blog.51cto.com/mister/2348637)

在`Ubuntu`系统操作过程中经常遇到一种情况，在命令行窗口输入数据，突然就不能输入了，好像这个命令行窗口卡死了

之前还以为是因为内存不足/`CPU`卡死/命令行窗口配置的问题，后来无意中在网上发现是因为无意中输入`ctrl+s`组合键，启动了窗口的锁屏功能

输入组合键`ctrl+q`即可解锁，**注意：锁屏期间仍旧能够输入，只是不显示而已**

## 问题四：[fcitx]重启输入法

不小心把输入法关闭了，之前有过好几回了，解决方法都是重启应用

找到一种解决方法，点击窗口键，输入`fcitx`，重新启动即可

## 问题五：[nautilus]重启文件管理器

今天遇到一个问题是文件夹突然打不开了，参考[ubuntu文件管理器假死的解决办法](https://blog.csdn.net/php_225869/article/details/73204533?utm_source=blogxgwz6)方法，查询文件管理器的`pid`并重启

    # 查找系统中的每个进程并搜索文件管理器nautilus
    $ ps -ef | grep nautilus
    zj        6938  1300  0 00:40 ?        00:00:01 /usr/bin/nautilus --gapplication-service
    zj        7822  7696  0 00:48 pts/2    00:00:00 grep --color=auto nautilus

然后杀死进程，重新点击文件夹启动

    kill 6938 & kill 7822
