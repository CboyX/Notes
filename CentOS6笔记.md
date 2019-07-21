### 级联创建目录

mkdir 将要创建的目录名称  -p

例子：在系统根目录下的var目录下创建temp目录以及该目录下的niginx目录

mkdir /var/temp/nginx -p



### 查看进程

* 查看全部进程

  ```shell
  ps aux
  ```

* 查看包含指定字符串的进程

  ```shell
  #查看包含字符串“nginx”的进程
  ps aux | grep nginx
  ```



### 杀掉进程

* 强行关闭进程

```shell
kill -9 进程的pid  
```

* 正常关闭进程

  ```shell
  kill 进程的pid  
  ```




### 查看端口

```shell
#查看全部被使用中的端口
netstat -lnp

#查看指定端口
netstat -lnp|grep 端口号
```



### 复制目录及该目录下的所有文件

```shell
cp -r 被复制的目录的名称 新目录名 
```



### 创建文件并添加文件内容

```sh
echo 文件内容 > 文件名
```



### 关机命令

##### [CentOS 6.5下关机与重启指令大全](https://blog.yayuanzi.com/6103.html)

```shell
Usage: ``shutdown` `[OPTION]... TIME [MESSAGE]
OPTION:选项
TIME:时间
MESSAGE:发送给所有使用者的警告信息
Options:
-r:将系统的服务停掉之后就重新启动
-h:将系统的服务停掉后，立即关机
-H:将系统的服务停掉后，立即关机(即-h)
-P:将系统的服务停掉后，立即关机(即-h)
-c:取消正在进行的关机进程
-k:仅仅发送警告信息，不是真的关机
```

```shell
shutdown` `-r now    立即重启
shutdown` `-h now    立即关机
shutdown` `-h 12:00 ``'I will shutdown'`    `系统在今天的12:00关机，若现在时间在12:00之后，则隔天的12:00再关机，并发送I wil ``shutdown``消息
shutdown` `-h +30    系统在30分钟后关机
```



### 关闭防火墙

暂时关闭防火墙，重启计算机后防火墙重新开启

```shell
service iptables stop
```

永久关闭防火墙

```shell
chkconfig iptables off
```

