### 开始看视频1-15

#### 1.SqlSession和connection（hibernate）都是非线程安全，所以不能声明在成员变量中

#### 2.mapper接口没有实现类，但是mybatis会为这个接口生成代理对象，将接口和XML文件进行绑定，从而可以使用代理对象来调用接口中的方法。

例子：

```java
EmployeeMaaper empMapper = sqlSession.getMapper(EmployeeMaaper.class);
--此时生成的empMapper 则为代理对象
```

#### 3.SqlSessionFactory可以由mybatis-config.xml这个*全局配置文件*创建，也可以不用mybatis-config.xml文件来创建，另外一种方式待续。。



#### 4.resource属性是引入类路径(classpath)下的资源，url属性是引入网络路径或者是磁盘路径下的资源。

注：类路径就是类似于IDEA中的Resource目录，类路径的根目录就是Resource目录中的第一级目录

例如：在mybatis-config.xml文件中引入外部属性文件

```xml
#该dbconfig.properties文件此时是放在类路径下的根目录
<properties resource="dbconfig.properties"></properties>

<properties url="d:/XX/XX/dbconfig.properties"></properties>
```





#### 5.别名

![1551360154548](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1551360154548.png)



#### 6.全局配置文件（mybatis-config.xml）中的`<mappers>`标签

* ##### 作用：将sql注入到全局配置中

* ##### 子标签:`<mapper>`

  * 作用是注册sql映射

    1. 通过注册配置文件来注册sql映射

    ​    例子：

    ```xml
    <mapper resource="mapper/EmployeeMapper.xml"></mapper>
    #注：此处是以resource属性来引入xml文件，也可以使用url的引入方式
    ```

    2. 通过注册接口来注册sql映射

       例子：

       ```xml
       <mapper class="mapper接口的全类名"></mapper>
       #注：这种引用方式下，映射文件名必须和接口同名(一般情况下都是同名的)，并且将映射文件放在与接口同目录下
       ```

    3. 批量注册

       批量注册情况下，要求映射文件名必须和接口同名(一般情况下都是同名的)，并且将映射文件放在与接口同目录下或者mapper接口的包名与XXmapper.xml文件的包名相同。

       ```xml
       <mapper packge="mapper接口的全类名"></mapper>
       ```

* ##### 子标签：`<package>`

  * 作用也是可以实现sql映射文件的批量引入

    批量注册情况下，要求映射文件名必须和接口同名(一般情况下都是同名的)，并且将映射文件放在与接口同目录下或者mapper接口的包名与XXmapper.xml文件的包名相同。

    例子：

    ```xml
    <package name="mapper接口的包名"></package>
    ```
