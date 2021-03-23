
# sudo使用

`sudo`允许系统管理员授予某些用户或用户组以根用户或其他用户身份运行命令的权限，同时提供对命令及其参数的审核跟踪

## 安装

```
apt-get install sudo
```

## 查询

查询当前用户的`sudo`配置

```
# sudo -ll
Matching Defaults entries for root on 326272a9a4eb:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User root may run the following commands on 326272a9a4eb:

Sudoers entry:
    RunAsUsers: ALL
    RunAsGroups: ALL
    Commands:
	ALL
```

查询指定用户的`sudo`配置

```
# sudo -lU zj
Matching Defaults entries for zj on 326272a9a4eb:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User zj may run the following commands on 326272a9a4eb:
    (ALL : ALL) ALL
```

* 参数`-l`表示列出用户权限或检查特定命令；使用两次`-ll`可获得更长的格式

* 参数`-U`表示在列表模式下显示用户的权限

## 解释

打开配置文件`/etc/sudoers`

```
# cat /etc/sudoers
#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root	ALL=(ALL:ALL) ALL
zj	ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo	ALL=(ALL:ALL) ALL

# See sudoers(5) for more information on "#include" directives:

#includedir /etc/sudoers.d
```

对于用户权限规范有

```
root	ALL=(ALL:ALL) ALL
zj	    ALL=(ALL:ALL) ALL
```

* 第一列表示用户名
* 第一个`ALL`表示允许从任何终端、机器访问`sudo`
* 第二个`ALL`表示`sudo`命令被允许以任何用户身份执行
* 第三个`ALL`表示`sudo`命令被允许以任何组身份执行
* 第四个`ALL`表示所有命令都可以作为`root`执行

对于组权限规范有

```
# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo	ALL=(ALL:ALL) ALL
```

## 修改

使用命令`visudo`进行配置文件的修改，其会先进行语法检查；或者使用编辑器配置完成后，执行以下命令进行语法检查

```
visudo -c -f /copy/of/sudoers
```

* 参数`-c`表示语法检查
* 参数`-f`表示指定文件位置

## 无密码运行sudo命令

修改`/etc/sudoers`文件如下

```
# 允许无密码执行echo和ls
zj ALL=(ALL) NOPASSWD: /bin/echo /bin/ls
# 允许无密码执行所有命令
zj ALL=(ALL) NOPASSWD: ALL
```

## 相关阅读

* [Sudo](https://wiki.archlinux.org/index.php/Sudo)

* [linux sudo 与 /etc/sudoer的配置](https://zhuanlan.zhihu.com/p/43934300)

* [Linux 系统中 sudo 命令的 10 个技巧](https://zhuanlan.zhihu.com/p/36037822)