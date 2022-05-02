
# 切换home目录到新硬盘

前几天尝试了将`home`目录切换到新安装的固态硬盘上，记录一下。

## 步骤

* 步骤一：安装新硬盘，初始化环境；
* 步骤二：同步数据到新硬盘；
* 步骤三：切换`home`目录到新硬盘。

## 操作

将新硬盘安装到主机，进行初始化后挂载到某一路径，拷贝`home`目录下数据后绑定`home`目录到新硬盘即可。

1. 查询新挂载的硬盘

        $ fdisk -l
        # 假定新硬盘名字为/dev/sda
        #
        # 初始化硬盘环境
        sudo mkfs.ext4 /dev/sda

2. 挂载到指定路径（临时目录）

        # 注：如果/data不存在需要提前新建
        $ sudo mkdir /data
        # 
        # sudo mount [--source] [--target]
        $ sudo mount /dev/sda /data
        # 
        # 数据同步
        $ rsync -av /home /data
        # 
        # 完成同步后解绑新硬盘和临时目录
        # sudo umount /data

3. 绑定`home`目录到新硬盘

        # 首先移动home目录
        # 有可能会出现移动失败的问题，原因在于有进程在后台操作，具体解决操作网上查询即可
        $ mv /home /home_old
        #
        # 挂载新硬盘到home目录
        $ sudo mkdir /home
        $ sudo mount /dev/sda /home
        #
        # 修改fstab文件，设置开机自动挂载
        $ sudo vim /etc/fstab
        # /etc/fstab: static file system information.
        #
        # Use 'blkid' to print the universally unique identifier for a
        # device; this may be used with UUID= as a more robust way to name devices
        # that works even if disks are added and removed. See fstab(5).
        #
        # <file system> <mount point>   <type>  <options>       <dump>  <pass>
        # / was on /dev/nvme0n1p2 during installation
        UUID=878a6311-c806-4ed8-84ea-c230b0774002 /               ext4    errors=remount-ro 0       1
        ...
        ...
        # 绑定新硬盘和home路径，同时设置为home目录
        /dev/sda          /home              ext4           default           0             2
        # 解绑原先home目录，同时设置为普通挂载
        /dev/sdb5      /home_old     ext4           default           0             0

完成上述操作后重启即可。另外，如何想要查询新硬盘对应`UUID`可以查看以下路径

```
$ ls -l /dev/disk/by-uuid/
```

## 相关阅读

* [Linux系统home目录挂载新硬盘并保存原目录下文件方法](http://dljz.nicethemes.cn/news/show-71224.html)