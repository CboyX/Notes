#### 1.级联创建目录

mkdir 将要创建的目录名称  -p

例子：在系统根目录下的var目录下创建temp目录以及该目录下的niginx目录

mkdir /var/temp/nginx -p



#### 2.查看进程

* 查看全部进程

  ```shell
  ps aux
  ```

* 查看包含指定字符串的进程

  ```shell
  #查看包含字符串“nginx”的进程
  ps aux | grep nginx
  ```



#### 3.杀掉进程

* 强行关闭进程

```shell
kill -9 进程的pid  
```

* 正常关闭进程

  ```shell
  kill 进程的pid  
  ```




#### 4.查看端口

```shell
#查看全部被使用中的端口
netstat -lnp

#查看指定端口
netstat -lnp|grep 端口号
```



#### 5.复制目录及该目录下的所有文件

```shell
cp -r 被复制的目录的名称 新目录名 
```



#### 6.创建文件并添加文件内容

```sh
echo 文件内容 > 文件名
```

