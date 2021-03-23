
# dash vs. bash

## dash

通常使用`sh`作为`shell`脚本的执行命令，其位于

```
$ which sh
/bin/sh
```

其是一个链接，指向

```
$ file /bin/sh
/bin/sh: symbolic link to dash
```

所以`dash`是默认解释器

```
$ file /bin/dash
/bin/dash: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/l, for GNU/Linux 2.6.32, BuildID[sha1]=504637666875a5d526ef51acfe601c99efc99114, stripped
```

## bash

在编写`shell`文件时，会在开头加上如下语句

```
#!/bin/bash
```

其含义是在没有指定解释器时，使用`/bin/bash`作为脚本解释器执行

```
$ file /bin/bash
/bin/bash: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/l, for GNU/Linux 2.6.32, BuildID[sha1]=6f072e70e3e49380ff4d43cdde8178c24cf73daa, stripped
```

## sh vs. dash vs. bash

* `sh`是一种编程语言，指的是`shell`命令语言，其规范由[POSIX standard](https://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html)指定
* `bash(the GNU Bourne-Again Shell)`和`dash(the Debian Almquist Shell)`是兼容`sh`规范的脚本解释器
* 对于`Debian`和`Ubuntu`系统而言，其默认的`sh`链接指向的是`dash`

`bash`能实现的功能比`dash`多，具体差别参考[bash和dash区别](https://blog.csdn.net/happycxz/article/details/78543187)，所以执行脚本时使用`bash`

```
$ bash test.sh
```

## 相关阅读

* [Difference between sh and bash](https://stackoverflow.com/questions/5725296/difference-between-sh-and-bash)

* [Ubuntu dash与bash的区别](https://blog.csdn.net/hansel/article/details/9817129)
