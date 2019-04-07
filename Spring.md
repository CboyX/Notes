## 开始看1-06

### Spring框架Runtime(运行时)环境

![1553610354727](assets/1553610354727.png)

由上图可看出，Spring涉及到了数据访问层和web层（controller层）以及业务层，所以能很好的和数据访问层的Mybatis以及web层的SpringMVC整合，以促进更加方便地使用Mybatis和SpringMVC。Spring在业务层上的表现是AOP和声明式事务等功能的体现。可以说Spring就是一个一站式的框架。

### Spring中需要学习的几大核心功能

IOC/DI

AOP

声明式事务



### IOC(控制反转)

* IOC完成的事情就是将原先由程序员手动new实例化对象的事情，转交给Spring负责。
* 控制反转中的控制指的是：控制类 的对象。
* 控制反转中的反转指的是：实例化对象交给Spring负责。
* IOC最大的作用就是`解耦`，程序员不需要管理对象，解除了程序员和管理对象之间的`耦合`.

### BeanFactory和ApplicationContext

ApplicationContext是BeanFactory的子接口。他们都可代表Spring容器，Spring容器是生成Bean实例的工厂，并且管理容器中的Bean。ApplicationContext在 BeanFactory 的基础上添加了其他功能，比如与 Spring 的 AOP 更容易集成，也提供了处理 message resource 的机制（用于国际化）、事件传播以及应用层的特别配置，比如针对 Web 应用的WebApplicationContext。BeanFactory 接口是 Spring IoC 容器的核心接口。

### Spring环境搭建（基于maven）

1. 创建maven项目

2. 添加Spring的核心依赖。

   要运行一个基本的Spring 必须要有的jar包有5个：`spring-beans`、`spring-core`、`spring-expression`、`spring-context`、`commons-logging`。在pom文件中添加依赖时，只要添加`spring-context`依赖即可，因为这个依赖中包含了其他几个的jar包。

3. 创建`applicationContext.xml`文件，并添加xsd约束。在IDEA中创建spring的`applicationContext.xml`时，会自动创建满足IOC所需要的基本xsd约束。

4. 到此spring环境已经搭建好，接下来就是创建JavaBean，然后就是将将写好的JavaBean配置到`applicationContext.xml`中。

5. 编写测试类，测试spring的IOC。

   ```java
   public class TestDemo {
       public static void main(String[] args) {
           //初始化spring容器
       ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
           //获取指定的容器中的对象
           People p = applicationContext.getBean("people", People.class);
   		//或是通过强转型的方式获取
           //People p = (People) applicationContext.getBean("people");
           System.out.println(p);
       }
   
   }
   ```

   运行该测试类，输出的结果为：

   ![1553870511824](assets/1553870511824.png)

   说明此时People对象是已经被Spring容器创建了，只是我自己没有给里面的属性赋值而已，说明IOC起了作用。



### Spring容器创建对象的三种方式

1. 通过构造方法创建

   1.1 无参构造创建（默认情况）

   1.2 有参构造创建（需要明确配置）

   ​	1.2.1 需要在`JavaBean`中创建有参构造函数

   ​	1.2.2 在`bean`标签中的`constructor-arg`子标签中设置调用哪个构造方法来创建对象，				如果`JavaBean`中存在多个参数类型相同，但是顺序不同的构造函数，那么以最后的那个构造函数来创建对象。

2. 实例工厂创建（需要先创建工厂对象，通过该工厂对象来创建相应的对象。类似非静态方法需要先创建对象才能被调用）

   2.1 工厂设计模式：帮助创建对象，通过传入不同的参数来让工厂创建不同的对象。

   2.2 实现步骤：

   * 创建一个工厂类

     ```java
     public class PeopleFactory {
     	public People newInstance(){
     		return new People(1,"测试");
     	}
     }
     ```

   * 在`applicationContext.xml`中配置工厂对象和所要创建的对象（此处是People对象）

     ```xml
     <bean id="factory" class="com.bjsxt.pojo.PeopleFactory"></bean>
     <bean id="peo1" factory-bean="factory" factory-method="newInstance"></bean>
     ```

   * 最后还是使用如下的方式来获取对象

     ```java
     ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
     		People people = ac.getBean("peo1",People.class);
     		System.out.println(people);
     ```

3. 静态工厂创建（不用创建工厂对象，即可直接通过工厂类直接创建相应的对象。类似静态方法不需要创建对象就能直接被调用）

   实现步骤：

   * 创建一个工厂类

     ```java
     public class PeopleFactory {
     	public static People newInstance(){
     		return new People(1,"测试2");
     	}
     }
     ```

   * 在`applicationContext.xml`中所要创建的对象

     ```xml
     <bean id="peo2" class="xx.xx.PeopleFactory" factory-method="newInstance"></bean>
     ```

   * 最后还是使用如下的方式来获取对象

     ```java
     ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
     		People people = ac.getBean("peo2",People.class);
     		System.out.println(people);
     ```



