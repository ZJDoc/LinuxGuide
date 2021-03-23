
# Apache Ant

官网下载[二进制包](http://ant.apache.org/bindownload.cgi)，需要预先安装好`JDK`

## 设置环境变量

修改`~/.bashrc`后刷新或重启即可

    $ vim ~/.bashrc
    # ant
    export ANT_HOME=/home/zj/software/ant/apache-ant-1.10.5
    export PATH=$PATH:$ANT_HOME/bin

## 测试

    $ ant -version
    Apache Ant(TM) version 1.10.5 compiled on July 10 2018

### 问题

    Unable to locate tools.jar

系统默认配置的`JDK`不太完善，需要重新安装`JDK`

## 相关阅读

* [Ubuntu 16.04中ant的安装和配置](https://blog.csdn.net/weiganliu/article/details/83089602)
* [Apache Ant运行时Unable to locate tools.jar解决方法](https://blog.csdn.net/xifeijian/article/details/8836438)