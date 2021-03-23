
# [Ubuntu 16.04]Cuda和Cudnn安装

之前已安装好了`Nvidia`显卡驱动，这一步安装`cuda`和`cudnn`

---

## cuda安装

参考：[Ubuntu16.04下安装cuda和cudnn的三种方法（亲测全部有效）](https://blog.csdn.net/wanzhen4330/article/details/81699769)

分`3`步：

1. 下载
2. 安装
3. 设置环境变量

### 下载

先下载对应`cuda`版本，官网下载：[CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)

我下载的是`.run`文件

### 安装

先授予权限

    sudo chmod 777 cuda*.run

直接运行即可

    sudo ./cuda*.run

首先显示一个应用许可（很长，可以按`'q'`键退出），然后会提示你输入是否允许

    Do you accept the previously read EULA?
    accept/decline/quit: accept

输入`accept`，然后提示你是否安装驱动，因为已经安装了，所以输入`no`

    Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 410.48?
    (y)es/(n)o/(q)uit: no

最后提示你安装

    Install the CUDA 10.0 Toolkit?
    (y)es/(n)o/(q)uit: yes

默认安装位置即可

    Enter Toolkit Location
    [ default is /usr/local/cuda-10.0 ]:

是否安装一个软链接，默认即可

    Do you want to install a symbolic link at /usr/local/cuda?
    (y)es/(n)o/(q)uit: yes

是否安装实例

    Install the CUDA 10.0 Samples?
    (y)es/(n)o/(q)uit: yes

可以选择实例位置，默认即可

    Enter CUDA Samples Location
    [ default is /home/zj ]: 

接下来就是安装过程了

    Installing the CUDA Toolkit in /usr/local/cuda-10.0 ...
    Missing recommended library: libGLU.so
    Missing recommended library: libX11.so
    Missing recommended library: libXi.so
    Missing recommended library: libXmu.so
    Missing recommended library: libGL.so

    Installing the CUDA Samples in /home/zj ...
    Copying samples to /home/zj/NVIDIA_CUDA-10.0_Samples now...
    Finished copying samples.

    ===========
    = Summary =
    ===========

    Driver:   Not Selected
    Toolkit:  Installed in /usr/local/cuda-10.0
    Samples:  Installed in /home/zj, but missing recommended libraries

    Please make sure that
    -   PATH includes /usr/local/cuda-10.0/bin
    -   LD_LIBRARY_PATH includes /usr/local/cuda-10.0/lib64, or, add /usr/local/cuda-10.0/lib64 to /etc/ld.so.conf and run ldconfig as root

    To uninstall the CUDA Toolkit, run the uninstall script in /usr/local/cuda-10.0/bin

    Please see CUDA_Installation_Guide_Linux.pdf in /usr/local/cuda-10.0/doc/pdf for detailed information on setting up CUDA.

    ***WARNING: Incomplete installation! This installation did not install the CUDA Driver. A driver of version at least 384.00 is required for CUDA 10.0 functionality to work.
    To install the driver using this installer, run the following command, replacing <CudaInstaller> with the name of this run file:
        sudo <CudaInstaller>.run -silent -driver

    Logfile is /tmp/cuda_install_6910.log

安装失败了，缺少一些库，需要安装相应的库，参考：[ubuntu 16.04 安装cuda 8 出现的错误：Missing recommended library: libGLU.so；Missing recommended library: libX](https://blog.csdn.net/qjk19940101/article/details/78927109)

    sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev

再重新安装

    sudo ./cuda_10.0.130_410.48_linux.run -silent -driver

### 设置环境变量

修改`.bashrc`文件

    sudo gedit ~/.bashrc

添加环境变量

    export PATH=$PATH:/usr/local/cuda-10.0/bin
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.0/lib64

更新环境变量

    source ~/.bashrc

查询版本

    zj@zj-ThinkPad-T470p:~$ nvcc --version
    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright (c) 2005-2018 NVIDIA Corporation
    Built on Sat_Aug_25_21:08:01_CDT_2018
    Cuda compilation tools, release 10.0, V10.0.130

还可以编译`cuda sample`来查询版本

    cd ~/NVIDIA_CUDA-10.0_Samples/1_Utilities/deviceQuery
    make
    ./deviceQuery

    ./deviceQuery Starting...

    CUDA Device Query (Runtime API) version (CUDART static linking)

    Detected 1 CUDA Capable device(s)

    Device 0: "GeForce 940MX"
    CUDA Driver Version / Runtime Version          10.0 / 10.0
    CUDA Capability Major/Minor version number:    5.0
    Total amount of global memory:                 2004 MBytes (2101870592 bytes)
    ( 3) Multiprocessors, (128) CUDA Cores/MP:     384 CUDA Cores
    GPU Max Clock rate:                            1189 MHz (1.19 GHz)
    Memory Clock rate:                             2505 Mhz
    Memory Bus Width:                              64-bit
    L2 Cache Size:                                 1048576 bytes
    Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
    Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
    Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
    Total amount of constant memory:               65536 bytes
    Total amount of shared memory per block:       49152 bytes
    Total number of registers available per block: 65536
    Warp size:                                     32
    Maximum number of threads per multiprocessor:  2048
    Maximum number of threads per block:           1024
    Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
    Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
    Maximum memory pitch:                          2147483647 bytes
    Texture alignment:                             512 bytes
    Concurrent copy and kernel execution:          Yes with 1 copy engine(s)
    Run time limit on kernels:                     No
    Integrated GPU sharing Host Memory:            No
    Support host page-locked memory mapping:       Yes
    Alignment requirement for Surfaces:            Yes
    Device has ECC support:                        Disabled
    Device supports Unified Addressing (UVA):      Yes
    Device supports Compute Preemption:            No
    Supports Cooperative Kernel Launch:            No
    Supports MultiDevice Co-op Kernel Launch:      No
    Device PCI Domain ID / Bus ID / location ID:   0 / 2 / 0
    Compute Mode:
        < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

    deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 10.0, CUDA Runtime Version = 10.0, NumDevs = 1
    Result = PASS

---

## `cudnn`安装

*需要注册一个账户才能下载`cudnn`*

到官网下载对应的包：[cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)

我的系统是`Ubuntu16.04`, 符合条件的有

    cuDNN Runtime Library for Ubuntu16.04 (Deb)
    cuDNN Developer Library for Ubuntu16.04 (Deb)
    cuDNN Code Samples and User Guide for Ubuntu16.04 (Deb)

下载完成后安装

    sudo dpkg -i libcudnn7*.deb

或者下载通用`linux`压缩包

    cuDNN Library for Linux

然后将文件复制到`cuda`安装路径下，参考：[How can I install CuDNN on Ubuntu 16.04?](https://askubuntu.com/questions/767269/how-can-i-install-cudnn-on-ubuntu-16-04)

### 验证cudnn

参考：[How to install CUDA and cuDNN on Ubuntu 16.04 LTS](https://blog.codingecho.com/2018/02/19/how-to-install-cuda-and-cudnn-on-ubuntu-16-04-lts/)

查询`cudnn`安装文件地址

    sudo updatedb
    locate cudnn

将测试文件复制到`home`目录下

    cp -r /usr/src/cudnn_samples_v7/ $HOME/cudnn_samples_v7/
    cd cudnn_samples_v7/mnistCUDNN/
    make clean && make
    ./mnistCUDNN

测试结果

    cudnnGetVersion() : 7401 , CUDNN_VERSION from cudnn.h : 7401 (7.4.1)
    Host compiler version : GCC 5.4.0
    There are 1 CUDA capable devices on your machine :
    device 0 : sms  3  Capabilities 5.0, SmClock 1189.0 Mhz, MemSize (Mb) 2004, MemClock 2505.0 Mhz, Ecc=0, boardGroupID=0
    Using device 0
    ...
    ...
    Test passed!

使用第二种复制`cudnn`文件方法的可以参考：[How to verify CuDNN installation?](https://stackoverflow.com/questions/31326015/how-to-verify-cudnn-installation)