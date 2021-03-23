
# [curl]网页调试

可以通过`curl`请求网页，查询部署是否成功

## 最简单的网页请求

```
$ curl www.baidu.com
# 可以指定http还是https
$ curl https://www.baidu.com
```

## 证书不受信

```
-k	允许curl使用非安全的ssl连接并且传输数据（证书不受信）
# 示例
$ curl -k http://xxx.xxx.xxx:7700
```

## 指定Http请求方法

默认为`Get`请求，使用参数`-X`指定

```
$ curl -X post http://xxx.xxx.xxx:7700
```

## 相关阅读

* [curl用法详解](https://www.cnblogs.com/lxyit/p/9173842.html)
