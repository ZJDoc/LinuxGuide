
# [Thinkpad T470p][Ubuntu 16.04]双显卡配置问题：无法切换显卡

原本`Thinkpad T470p`预装的是`win10`家庭版，有双显卡，可以通过`NVIDIA Settings`进行显卡切换

现在将系统重装为`Ubuntu`，发现双显卡的配置和想象的不一样

    zj@zj-ThinkPad-T470p:~$ lspci | grep -i -E "vga|3d"

    00:02.0 VGA compatible controller: Intel Corporation Device 591b (rev 04)
    02:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev a2)

`Intel`显卡的名称为`VGA compatible controller`，而`NVIDIA`显卡的名称为`3D controller`

安装`NVIDIA`显卡驱动后，能够运行`nvidia-smi`但是不能运行`nvidia-settings`，以及图形应用`NVIDIA X Server Settings`

    zj@zj-ThinkPad-T470p:~$ nvidia-smi 
    Mon Jan 14 19:34:28 2019       
    +-----------------------------------------------------------------------------+
    | NVIDIA-SMI 410.93       Driver Version: 410.93       CUDA Version: 10.0     |
    |-------------------------------+----------------------+----------------------+
    | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    |===============================+======================+======================|
    |   0  GeForce 940MX       Off  | 00000000:02:00.0 Off |                  N/A |
    | N/A   32C    P8    N/A /  N/A |     11MiB /  2004MiB |      0%      Default |
    +-------------------------------+----------------------+----------------------+
                                                                                
    +-----------------------------------------------------------------------------+
    | Processes:                                                       GPU Memory |
    |  GPU       PID   Type   Process name                             Usage      |
    |=============================================================================|
    |  No running processes found                                                 |
    +-----------------------------------------------------------------------------+

    zj@zj-ThinkPad-T470p:~$ nvidia-settings 

    ERROR: Unable to load info from any available system

在网上找了许多资料，发现是因为`t470p`使用了`NVIDIA Optimus`技术，默认在正常使用时基于集显，在玩游戏时基于独显，参考：[NVIDIA® Optimus™ 技术](https://www.nvidia.cn/object/optimus_technology_cn.html)

在`win10`环境下还能切换，但在`Ubuntu`环境下无法设置了


