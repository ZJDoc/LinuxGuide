
# 删除陈旧的APT仓库

## 问题复现

使用`apt-get update`更新时发生如下错误

```
$ sudo apt-get update
...
...
Ign:27 http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial/main DEP-11 64x64 Icons
Err:21 http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial/main amd64 Packages
  404  Not Found [IP: 91.189.95.83 80]
...
...
Err:30 https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu xenial/main Sources
  404  Not Found
...
...
Fetched 8,289 B in 6min 42s (20 B/s)
Reading package lists... Done
W: The repository 'http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial Release' does not have a Release file.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
W: The repository 'https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu xenial Release' does not have a Release file.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: Failed to fetch http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu/dists/xenial/main/binary-amd64/Packages  404  Not Found [IP: 91.189.95.83 80]
E: Failed to fetch https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/dists/xenial/main/source/Sources  404  Not Found
E: Some index files failed to download. They have been ignored, or old ones used instead.
```

## 问题解决

需要移除对应的仓库链接

### 命令行方式

```
$ sudo add-apt-repository --remove ppa:t-tujikawa/ppa
```

### 文件编辑方式

进入`/etc/apt/sources.list.d`，查找对应的文件

```
$ cat t-tujikawa-ubuntu-ppa-xenial.list
deb http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial main
# deb-src http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial main
$ cat t-tujikawa-ubuntu-ppa-xenial.list.save 
deb http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial main
# deb-src http://ppa.launchpad.net/t-tujikawa/ppa/ubuntu xenial main
```

删除文件或删除里面的内容

## 相关阅读

* [Linux教程：如何查找并移除Ubuntu上陈旧的PPA仓库](https://www.linuxidc.com/Linux/2014-09/107055.htm)

* [Ubuntu update 出现错误的安装源](https://juejin.im/post/5b41abc25188251acb0cd8cd)

* [Ubuntu 16.04系统下出现E: 无法下载 http://ppa.launchpad.net/fcitx-team/nightly/ubuntu/dists/xenial/main/binary-amd64/Packages 404 Not Found](https://www.cnblogs.com/wenzheshen/p/6599636.html)

