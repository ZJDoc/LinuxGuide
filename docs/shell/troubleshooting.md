
# 问题解答

## 问题一：[[: not found

使用`sh`命令执行脚本`test.sh`

```
$ cat test.sh 
#!/bin/bash

NAME="asdf asdf as"

if [[ ${NAME} == as* ]]
then
	echo "匹配"
else
	echo "不匹配"
fi
```

得到问题如下：

```
$ sh test.sh 
test.sh: 5: test.sh: [[: not found
不匹配
```

原因是相比较于`bash`而言，`dash`的功能少，无法解析`[[ ]]`，使用`bash`执行即可

```
$ bash test.sh 
匹配
```