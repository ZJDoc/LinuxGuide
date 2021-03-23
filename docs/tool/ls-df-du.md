
# [ls][df][du]查看文件、目录、文件系统大小

经常需要判断文件、文件夹和磁盘空间的大小，总结一下

常用命令包括：

1. `ls`：列出目录内容
2. `df`：报告文件系统磁盘空间使用情况
3. `du`：估计文件空间使用率

## 查看文件、文件夹大小

### 使用ls命令查看文件大小

查看指定目录下文件大小(**不包含隐藏文件**)

    # 当前目录
    $ ls -sh
    总用量 727M
    4.0K blogs  4.0K git  4.0K opencv  4.0K opencv_contrib  183M opencv_contrib.tar.gz  544M opencv.tar.gz
    # 指定目录
    $ ls -sh opencv
    总用量 116K
    4.0K 3rdparty  4.0K apps  4.0K cmake   68K CMakeLists.txt  4.0K CONTRIBUTING.md  4.0K data  4.0K doc  4.0K include  4.0K LICENSE  4.0K modules  4.0K platforms  4.0K README.md  4.0K samples

查看指定文件大小

    $ ls -sh opencv.tar.gz
    544M opencv.tar.gz

参数`-s`表示以块为单位打印每个文件的分配大小

    -s, --size
    print the allocated size of each file, in blocks

参数`-h`表示打印人类可读大小

    -h, --human-readable
    with -l and/or -s, print human readable sizes (e.g., 1K 234M 2G)

**如果要查看目录下隐藏文件大小，可以增加参数`-a`**

参数`-a`表示不忽略隐藏文件（以点号开头）

    -a, --all
    do not ignore entries starting with .

### 使用sh命令查看文件、文件夹大小

查看当前目录下文件和文件夹大小

    $ du -sh *
    3.2M	blogs
    7.8M	git
    646M	opencv
    237M	opencv_contrib
    183M	opencv_contrib.tar.gz
    544M	opencv.tar.gz

查看指定文件或文件夹大小

    # 指定文件
    $ du -sh opencv/CMakeLists.txt 
    68K	opencv/CMakeLists.txt
    # 指定文件夹
    $ du -sh opencv
    646M	opencv

参数`-s`表示只显示每个参数总的大小

    -s, --summarize
    display only a total for each argument

参数`-h`表示打印人类可读大小

    -h, --human-readable
    with -l and/or -s, print human readable sizes (e.g., 1K 234M 2G)

## 查看文件系统磁盘空间使用情况

命令`df`用于显示包含每个文件名参数的文件系统上可用的磁盘空间量，默认磁盘空间以`1K`块为最小单位。

    $ df -h
    文件系统        容量  已用  可用 已用% 挂载点
    udev            413M     0  413M    0% /dev
    tmpfs            87M  9.3M   78M   11% /run
    /dev/vda1        50G  3.5G   44G    8% /
    tmpfs           433M   24K  433M    1% /dev/shm
    tmpfs           5.0M     0  5.0M    0% /run/lock
    tmpfs           433M     0  433M    0% /sys/fs/cgroup
    tmpfs            87M     0   87M    0% /run/user/500
    # 或
    $ df -H
    文件系统        容量  已用  可用 已用% 挂载点
    udev            433M     0  433M    0% /dev
    tmpfs            91M  9.8M   81M   11% /run
    /dev/vda1        53G  3.8G   47G    8% /
    tmpfs           454M   25k  454M    1% /dev/shm
    tmpfs           5.3M     0  5.3M    0% /run/lock
    tmpfs           454M     0  454M    0% /sys/fs/cgroup
    tmpfs            91M     0   91M    0% /run/user/500

参数`-h`表示打印人类可读大小，以`1024`为单位

    -h, --human-readable
    print sizes in powers of 1024 (e.g., 1023M)

参数`-H`同样表示打印人类可读大小，以`1000`为单位

    -H, --si
    print sizes in powers of 1000 (e.g., 1.1G)
