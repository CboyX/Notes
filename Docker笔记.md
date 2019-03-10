#### 1.使用Docker for windows的注意事项

* 必须开启电脑中的Hyper-V功能

  ![1548404170536](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1548404170536.png)

#### 2.docker常用命令（CnetOS环境下）

* 启动docker服务

  ```she
  systemctl start docker
  ```

* 拉取镜像

  ```shll
  docker pull 镜像名称:版本号
  ```

* 创建并启动容器

  方式一：交互式（在创建容器并启动容器的同时会直接进入到容器）

  ```shell
  docker run -it --name=创建的容器名 镜像名:版本号 /bin/bash
  ```

  方式二：守护式（在创建容器并启动容器的不会进入到容器）

  ```shell
  docker run -id --name=创建的容器名 镜像名:版本号
  ```

* 退出或者是退出并关闭容器（**注意：只有当该容器是交互式创建，且第一次使用exit命令时，此时意味着退出并关闭容器，其他情况都只是退出容器的操作**）

  ```shell
  exit
  ```

* 查看正在运行的容器

  ```shell
  docker ps
  ```

* 查看所有的容器

  ```shell
  docker ps -a
  ```

* 启动已存在的容器

  ```shell
  docker start 容器名
  ```

* 启动并进入已存在的容器

  ```shell
  docker start 容器名 -i
  ```

* 进入已经启动的容器

  ```shel
  docker exec -it 容器名 /bin/bash
  ```

* 关闭容器

  ```shell
  docker stop 容器名
  ```

* 文件拷贝

  从宿主机拷贝到容器

  ```shell
  docker cp 文件名 容器名:容器内的目标目录
  ```

  例子：将宿主机当前目录下的testfile文件拷贝到容器centos7-03的/usr/local目录下

  ```shell
  docker cp testfile centos7-03:/usr/local
  ```



  从容器拷贝到宿主机

  ```shell
  docker cp 容器名:文件的目录/文件名 新文件名
  ```

  例子：将容器centos7-03中/usr/local目录下的testfile文件拷贝到此时宿主机所在的当前目录，并重新命名为testf

  ```shell
  docker cp centos7-03:/usr/local/testfile testf
  ```





  注意：容器之间不能直接进行文件的拷贝

* 目录挂载（也叫数据卷）：将宿主机中的某个目录**映射**到容器中的某个目录​	

  创建容器时挂载目录（此处创建的是守护式容器）

```shell
docker run -id -v 宿主机目录:容器目录 --privileged=true --name=创建的容器名 镜像名:版本号
```

--*privileged=true*  这句话指的是开启挂载目录下多级目录的访问权限

**注意：如果目录不存在，则自动创建该目录**，还有就是宿主机目录和容器目录是双向维护的，即修改一边，另外一边也会随之被修改



* 查看容器IP

  ```shell
  docker inspect 容器名
  ```

  注意：**容器的IP是启动容器时动态分配**的，未启动的容器没有IP

* 使用commit生成镜像

  ```shell
  docker commit 容器名 所要生成的镜像名
  ```

* 镜像的备份

  将镜像打包（打包后即可发送给其他人使用）

  ```shell
  docker save -o 包名.tar 镜像名
  ```

* 镜像的恢复

  使用别人打包好的镜像

  ```shell
  docker load -i 包名.tar
  ```

  再次查看docker中的镜像，此时就多了一个刚刚恢复镜像了。

* 使用Dockerfile生成镜像

  未完待续。。。

* 使用commit与Dockerfile的区别

  未完待续。。。

* 使用Docker-compose批量创建并启动和停止容器

  首先要创建一个docker-compose.yml文件

  然后再在该文件中添加相应配置，例子如下

  ![1550293661830](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1550293661830.png)

  其他标签：

  目录挂载

  **volumes:**

  ​        **- /usr/local/docker/tomcat/webapps:/usr/local/tomcat/test**



  写好docker-compose.yml文件后，接着就是启动该文件了，**注意：以下的所有docker-compose操作都必须在含有docker-compose.yml文件的目录中执行**。

  ```shell
  docker-compose up #前台创建启动,该启动就是将文件内所配置的所有容器全部启动 
  ```

  ```shell
  docker-compose up -d #后台创建并启动
  ```

  ```shell
  docker-compose start  #启动所有
  ```

  ```shell
  ctrl+C  #停止所有容器（仅适用于其前台启动）
  ```

  ```shell
  docker-compose stop #停止所有容器
  ```



  ```shell
  docker-compose down #停止并移除容器
  ```

* 查看docker-compose的启动日志

  ```shell
  docker-compose logs -f 服务名（也可以是容器名）
  ```


