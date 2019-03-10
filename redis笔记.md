#### 1.五种数据类型



#### 2.查看内存中所有的key

```shell
keys *
```

#### 3.设置key的过期时间

```shell
expire key的名称 秒数（多少秒后过期）
```

#### 4.查看指定key的过期时间

```shell
ttl key名称
```

key的过期时间若为 **-1**，则表示该key是持久化的；

若为 **-2** ，则表示不存在该key;若为其他 **正整数**，则表示该key的存活时间。

将非持久化的key转换成持久化:

```shell
Persist key名称
```





#### 5.使用客户端redis-cli连接已开启的redis（包括本地和远程的redis）,

* 连接本地redis

```shell
./redis-cli  #此处已经在bin目录下，所以是写的./
```

* 连接远程redis

  ```shell
  ./redis-cli -h 远程主机的ip -p 远程主机的redis端口号
  ```


