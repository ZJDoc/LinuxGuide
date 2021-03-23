
# Java

## 下载

官网地址：[Java Linux](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

### wget下载

直接复制下载地址然后使用`wget`下载会出错

    wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" + 右键复制的链接

## 设置环境变量

修改文件`/etc/profile`，添加如下环境变量后重启即可

    $ sudo vim /etc/profile
    # JAVA
    export JAVA_HOME=/home/zj/software/java/jdk1.8.0_201
    export JRE_HOME=$JAVA_HOME/jre
    export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
    export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

## 修改系统默认JDK

系统默认安装了`OpenJDK`，可以设置成`SunJDK`。首先添加`SunJDK`命令到`update-alternatives`

```
$ sudo update-alternatives --install /usr/bin/java java /home/zj/software/java/jdk1.8.0_201/bin/java 300

$ sudo update-alternatives --install /usr/bin/javac javac /home/zj/software/java/jdk1.8.0_201/bin/javac 300
update-alternatives: using /home/zj/software/java/jdk1.8.0_201/bin/javac to provide /usr/bin/javac (javac) in auto mode

$ sudo update-alternatives --install /usr/bin/jar jar /home/zj/software/java/jdk1.8.0_201/bin/jar 300
update-alternatives: using /home/zj/software/java/jdk1.8.0_201/bin/jar to provide /usr/bin/jar (jar) in auto mode

$ sudo update-alternatives --install /usr/bin/javah javah /home/zj/software/java/jdk1.8.0_201/bin/javah 300
update-alternatives: using /home/zj/software/java/jdk1.8.0_201/bin/javah to provide /usr/bin/javah (javah) in auto mode

$ sudo update-alternatives --install /usr/bin/javp javap /home/zj/software/java/jdk1.8.0_201/bin/javap 300
update-alternatives: using /home/zj/software/java/jdk1.8.0_201/bin/javap to provide /usr/bin/javp (javap) in auto mode
```

添加了`java/javac/jar/javah/javap`,有些是系统没有配置的,比如`javac/jar/javah/javap`,有些是系统已有配置的,比如`java`

然后设置`SunJDK`命令为指定配置

    $ sudo update-alternatives --config java
    There are 2 choices for the alternative java (providing /usr/bin/java).

    Selection    Path                                            Priority   Status
    ------------------------------------------------------------
    * 0            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      auto mode
    1            /home/zj/software/java/jdk1.8.0_201/bin/java     300       manual mode
    2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

    Press <enter> to keep the current choice[*], or type selection number: 1   
    update-alternatives: using /home/zj/software/java/jdk1.8.0_201/bin/java to provide /usr/bin/java (java) in manual mode

    $ sudo update-alternatives --config javac
    There is only one alternative in link group javac (providing /usr/bin/javac): /home/zj/software/java/jdk1.8.0_201/bin/javac
    Nothing to configure.

## 测试

    $ java -version
    java version "1.8.0_201"
    Java(TM) SE Runtime Environment (build 1.8.0_201-b09)
    Java HotSpot(TM) 64-Bit Server VM (build 25.201-b09, mixed mode)
    $ javac -version
    javac 1.8.0_201

## 相关阅读

* [如何用wget下载jdk](https://blog.csdn.net/lwgkzl/article/details/79889983)
* [ubuntu18.04 安装java](https://blog.csdn.net/sangewuxie/article/details/80958611)
* [Ubuntu18.04安装和配置 Java JDK 和 JRE，并卸载自带OpenJDK](https://blog.csdn.net/freeking101/article/details/80522586)