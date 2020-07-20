---
title: Spring-Learning-Notes
date: 2020-01-23 23:23:16
tags: [笔记, ssm, java, spring]
---

Spring Learning Notes

Spring个人学习笔记([建议](#advice)) 

part1 初识
--------------------------------------

### what

 大管家Spring是于2003 年兴起的一个轻量级的Java 开源框架，它由Rod
Johnson创建。传统J2EE应用的开发效率低，Spring作为开源的中间件，提供J2EE应用的各层的解决方案，Spring贯穿了表现层、业务层及持久层，而不是仅仅专注于某一层的方案。可以说Spring是企业应用开发的“一站式（full-stack）”选择。然而，Spring并不想取代那些已有的框架，而是与它们无缝地整合。

简单来说，Spring是一个轻量级**控制反转**(IoC)和**面向切面**(AOP)的**容器**框架。

<!--more-->

### why

**1、** **方便解耦，简化开发**

通过Spring提供的IoC容器，我们可以将对象之间的依赖关系交由Spring进行控制，避免硬编码所造成的过度程序耦合。有了Spring，用户不必再为单实例模式类、属性文件解析等这些很底层的需求编写代码，可以更专注于上层的应用。

**2、** **AOP编程的支持**

通过Spring提供的AOP功能，方便进行面向切面的编程，许多不容易用传统OOP实现的功能可以通过AOP轻松应付。

**3、** **声明式事务的支持**

在Spring中，我们可以从单调烦闷的事务管理代码中解脱出来，通过声明式方式灵活地进行事务的管理，提高开发效率和质量。

**4、** **方便程序的测试**

可以用非容器依赖的编程方式进行几乎所有的测试工作，在Spring里，测试不再是昂贵的操作，而是随手可做的事情。例如：Spring对Junit4支持，可以通过注解方便的测试Spring程序。

**5、** **方便集成各种优秀框架**

Spring不排斥各种优秀的开源框架，相反，Spring可以降低各种框架的使用难度，Spring提供了对各种优秀框架（如Struts、Hibernate、MyBatis
、Hessian、Quartz）等的直接支持。

**6、** **降低Java EE API的使用难度**

Spring对很多难用的Java EE
API（如JDBC，JavaMail，远程调用等）提供了一个薄薄的封装层，通过Spring的简易封装，这些Java
EE API的使用难度大为降低。

### learn what

1、 了解Spring框架、IOC、DI的概念；

2、 掌握Spring框架搭建、配置与使用；

3、 掌握Spring容器创建与对象管理；

4、 掌握Spring xml配置式开发与注解开发；

5、 掌握Spring AOP相关知识；

6、 掌握SpringJDBC相关知识；

7、 将Spring集成项目中进行测试；

以上三个段为截取他人文档–\>

[siki](http://www.sikiedu.com/my/course/267)

part2 Spring框架介绍与入门案例
--------------------------------------------------------------------------------------------------

![Spring](https://github.com/ZephXu07/IMG/raw/master/Spring.png)

### 1、 搭建Spring HelloWorld项目

a)
[Spring下载地址](http://repo.spring.io/release/org/springframework/spring/)

b) 导包：（以下5个包称为基本包）

 i. 核心包：bean、context、core、expression；

 ii. 日志包：apache.commons.logging

 **！！！maven项目中在pom.xml文件中加入dependency**

c) 引入约束：bean约束和引入主配置文件头；

```xml
  <?xml version="1.0" encoding="UTF-8"?>
  	<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.springframework.org/schema/beans" xsi:schemaLocation="http://www.springframework.org/schema/beans       http://www.springframework.org/schema/beans/spring-beans.xsd ">   
</beans>             |
```



-   **BUG：org.springframework.beans.factory.xml.XmlBeanDefinitionStoreException:
    Line 3 in XML document from class path resource
    [applicationContext.xml] is invalid; nested exception is
    org.xml.sax.SAXParseException; lineNumber: 3; columnNumber: 59;
    已经为元素 “beans” 指定属性 “xmlns”。**

-   **配置文件写错！**

![bugRepaired](https://github.com/ZephXu07/IMG/raw/master/BUG%E4%BF%AE%E6%94%B9.png)

d) 测试：将自定义对象由自己创建交由Spring管理；

- 项目结构：

  ![项目结构](https://github.com/ZephXu07/IMG/raw/master/SpringProjectStructure.png)

- 没使用Spring之前：自己new

  ````java
  @Test    
  public void Test() {
  	User u = new User();        
  	System.out.println(u);    
  }             |
  ````

- 使用Spring容器：spring帮忙管理对象

  - 配置：`<bean name="user" class="com.zephxu.bean.User"/>`

    ```java
    @Test
    public void Test2() {    //根据spring配置文件获取容器对象    
    	ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");//从spring容器中使用getBean取对象   
        User user1 = (User) ac.getBean("user");
        User user2 = ac.getBean(User.class);    
        System.out.println(user1 + "\n" + user2);
    }                         
    ```

    

### 2、Spring-IoC | DI概念介绍：（要实现IOC依赖DI的支持）

**IoC（Inversion of Control）：编程思想，新的设计模式。**

-   反转控制：将我们自己创建对象的工作交给Spring容器帮我们完成；
-   反转：创建对象这份工作由我们自己执行反转给Spring帮我们执行。
-   控制：由Spring负责创建销毁对象，掌控对象的生命周期等，需要使用时向Spring申请即可。

**DI（Dependency
Injection）：依赖注入：将值通过配置的方式为变量初始化/赋值(注入)**

c) 注入方式：set方法注入、构造注入、字段注入(不推荐)；

d) 注入类型：

 i. 值类型(value) – 八大基本数据类型；

 ii. 引用类型(ref) – String、自定义对象；

`<property name="u_id" value="7"/>`

```java
 User user1 = (User) ac.getBean("user");
 User user2 = ac.getBean(User.class);
 System.out.println(user1 + "\n" + user2);
 System.out.println(user1 == user2);      
```

**结果如下，原因未知……**

![未知原因](https://github.com/ZephXu07/IMG/raw/master/zephxu-Snipaste_2019-09-28_16-29-59.png)

**原因：**[Scope属性singleton单例](#锚1)

part3 Spring配置 
--------------------------------------------------------

### 1、XML配置

 a) Bean元素：交由Spring管理的对象都要配置在bean标签中；

 i. Bean标签介绍和创建方式：**空参构造（常用）**、静态工厂、动态工厂；

 （1）标签介绍：


一、name：起一个名字，通过其来利用容器获取对象；可以使用特殊字符；可以重复但不推荐。

 二、id：与name作用基本相似，但不推荐使用；不支持特殊字符；不能重复。

 三、class：被管理的对象的全包名，Spring通过此包名来创建对象。

 （2）空参构造：默认，若没有空参方法会报错。

 一、`public  User() {    System.out.println("User空参构造方法");}`

![.](https://github.com/ZephXu07/IMG/raw/master/zephxu-Snipaste_2019-09-28_16-53-26.png)


二、ApplicationContext配置的所有bean对象都会在容器被创建的时候创建出来，如果配置的bean较多，在创建容器的时候会产生内存过大问题，在硬件性能落后体现明显。

 **Spring提供开关解决问题：延迟加载**

![延迟加载](https://github.com/ZephXu07/IMG/raw/master/zephxu-Snipaste_2019-09-28_17-04-17.png)

 ii. Scope属性介绍：singleton、protoptype、request、session；

-   上面bug原因：singleton单例，为默认，只创建单个对象，一般项目
    ![singleton](https://github.com/ZephXu07/IMG/raw/master/zephxu-Snipaste_2019-09-28_21-22-24.png)

-   prototype，多例，相对singleton而言，在获取的时候创建新的对象，特殊项目

```java
User user1 = (User) ac.getBean("user");
User user2 = ac.getBean(User.class);
System.out.println(user1 + "\n" + user2);
System.out.println(user1 == user2);             
```



![prototype](https://github.com/ZephXu07/IMG/raw/master/zephxu-Snipaste_2019-09-28_21-29-03.png)

- request：在web环境下，如果scope属性为request，那么这个对象的生命周期与request请求一致。

- session：同理。

  iii. 项目有需求时在标签中有初始化方法init-method和
  销毁方法destroy-method；

  -   `init-method="userInit" destroy-method="userDestroy"`
  -   **容器关闭后激活destroy方法，当scope配置不是singleton而是prototype时，销毁方法不会被调用。**
  -   **init方法在容器创建Bean对象之后立即调用，destroy方法在容器销毁对象之前调用的，而使用prototype的话对象是由用户管理的。**

 b) 属性注入：

 i. Set方法注入：**bean对象中需要有对应的set方法！**

```xml
<!--将user对象交给Spring管理并注入值类型-->
<bean name="user" class="com.zephxu.bean.User">    
	<property name="u_id" value="999"/> 
    <property name="u_username" value="黄源钦"/>
    <property name="u_password" value="511"/>    
    <!--引用类型注入方式-->    
    <property name="u_pet" ref="cat"/>
</bean>
<!--注入引用类型使用ref，注入值类型使用value-->
<!--注入引用类型-->
<bean name="cat" class="com.zephxu.bean.Pet">        
	<property name="petType" value="狸花猫"/>        
	<property name="color" value="黑白相间"/>
</bean>    |
```

 ii. 构造函数注入；

bean对象中：

```java
public User(String u_username, Pet u_pet) {   
	System.out.println("方法1：String, Pet");    
	this.u_username = u_username;    
	this.u_pet = u_pet;
}                                    
```

配置xml文件中：java

```xml
<!--构造方法注入-->
<bean name="user1" class="com.zephxu.bean.User">   
    <!--name为调用构造器中的参数名-->    
    <constructor-arg name="u_username" value="咸鱼"/>
    <constructor-arg name="u_pet" ref="cat"/>
</bean>                   
```



**调用时需要使用使用xml文件中配置的特定的bean对象的name而不是使用User.class。（下面BUG的原因之一）**

```java
public void Test2() {    
	ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContextInjection.xml");
    User user = (User)ac.getBean("user1");//！此处需要注意！    
    System.out.println(user);
}  
```



**注意：当有参构造器有多个时，如下：**

bean对象：

```java
public User(String u_username, Pet u_pet) {        
    System.out.println("方法1：String, Pet");        
    this.u_username = u_username;        
    this.u_pet = u_pet;
}
public User(Integer u_username, Pet u_pet) {  
    System.out.println("方法2：Integer, Pet");  
    this.u_username = u_username.toString(); 
    this.u_pet = u_pet;
}
public User(Pet u_pet, Integer u_username) {   
    System.out.println("方法3：Pet, Integer");
    this.u_username = u_username.toString(); 
    this.u_pet = u_pet;
}            
```



xml文件：

```xml
<bean name="user1" class="com.zephxu.bean.User">    
<!--type可以指定参数类型，index可以指定参数的位置，以0下标开始，使用这两个属性来调用想要的 构造器-->    
<constructor-arg name="u_username" value="777" type="java.lang.Integer" index="1"/>
<constructor-arg name="u_pet" ref="cat"/>
</bean>                                    
```



 iii. 复杂类型注入：Array、List、Set、Map、Properties

```xml
<!--复杂类型的注入-->
<bean name="collection" class="com.zephxu.bean.MyCollection">    
    <!--array-->    
    <property name="array">        
        <array><!--数组类型特有的标签，注入对象-->          
            <value>phy</value>            
            <value>xzf</value>
            <ref bean="cat"/><!--同上value和ref标签用法-->            
            <!--当一个值时可以<property name="array" value="123>-->       
        </array>    
    </property>
    <!--list-->    
    <property name="list">        
        <list>            
            <value>phy</value>            
            <value>xzf</value>            
            <ref bean="cat"/>
            <ref bean="user"/>
            <ref bean="user1"/>        
        </list>   
    </property>    
    <!--set-->
    <property name="set">
        <set>
            <value>phy</value>
            <value>xzf</value>            
            <ref bean="cat" />            
            <ref bean="user" />            
            <ref bean="user1" />        
        </set>    
    </property>    
    <!--list，set用法同array-->    
    <!--map特殊-->    
    <property name="map">
        <map>            
            <entry key="username" value="root"/>            
            <entry key="userpassword" value="10709991"/> 
            <entry key-ref="user1" value-ref="cat"/>       
            <!--依据Map的用法，需要键值对-->        
        </map>
    </property>    
    <!--properties-->
    <property name="prop">        
        <props>            
            <prop key="boy">xzf</prop>            
            <prop key="girl">phy</prop>            
            <!--类似键值对，但值是写在标签中-->        
        </props>    
    </property>
</bean>                              
```

**BUG：No qualifying bean of type ‘com.zephxu.bean.User’ available:
expected single matching bean but found 2: user,user1**

**原因：[如上；](#锚2)**

### 2、注解配置 

a) 导包和约束：基本包、aop包+context约束；

maven的pom.xml文件：

```xml
<dependency>    
    <groupId>org.springframework</groupId>    
    <artifactId>spring-aop</artifactId>   
    <version>5.1.10.RELEASE</version>
</dependency> 
```

applicationContext.xml文件中：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.springframework.org/schema/beans" xmlns:context="http://www.springframework.org/schema/context"       xsi:context="http://www.springframework.org/schema/context"       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">   
    <!--注解开发-->    <!--开启组件扫描 base-package 扫描该包下以及子包的所有注解-->    <context:component-scan base-package="com.zephxu.bean"/>
</beans>
```



b) 将对象注册到容器内；

c) 用注解配置Scope属性；

d) 注解配置init-method与destroy-method；

**注解：**

```java
@Component("user2")
@Scope(scopeName="singleton")//prototype
//在构造方法后调用@PostConstruct
//在销毁方法前调用@PreDestroy
```

**等于xml中：**

```xml
<bean name="user2" class="com.zephxu.bean.User2" init-method="user2Init" destroy-method="user2Destroy">
```

- 注意：

```java
@Controller()//web层
@Service()//service层
@Repository()//dao层    
```

e） 注解配置属性注入，值类型与引用类型；

```java
@Value(value = "1226")
private Integer u_id;//使用暴力反射注入@Value("🐠")
//推荐在set方法上使用
public void setU_username(String u_username) { 
	this.u_username = u_username;
}
//@Autowired//自动装配，只适用于一个Pet对象时
@Resource(name = "老奶猫")
public void setU_pet(Pet u_pet) {   
	this.u_pet = u_pet;
}              
```



### 3、 Spring & JUnit进行测试：

a) 导包： test包（依赖 aop包）；

b) 使用@RunWith注解创建spring容器；

c） 使用@ContextConfiguration读取spring配置文件

````java
 @RunWith(SpringJUnit4ClassRunner.class)
 //使用junit进行测试，帮助创建容器
 @ContextConfiguration("classpath:applicationContextInjection.xml")
 //读取配置文件
 publicclass TestJunit {    
 	@Resource(name = "cat")    
 	private Pet pet;   
    @Test    
    public void test() {        
    System.out.println(pet); 
    }
}          
````



**BUG：**java.lang.ExceptionInInitializerError\
 at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native
Method)\
 at
sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)\
 at
sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)\
 at java.lang.reflect.Constructor.newInstance(Constructor.java:423)\
 at
org.junit.internal.builders.AnnotatedBuilder.buildRunner(AnnotatedBuilder.java:29)\
 at
org.junit.internal.builders.AnnotatedBuilder.runnerForClass(AnnotatedBuilder.java:21)\
 at
org.junit.runners.model.RunnerBuilder.safeRunnerForClass(RunnerBuilder.java:59)\
 at
org.junit.internal.builders.AllDefaultPossibilitiesBuilder.runnerForClass(AllDefaultPossibilitiesBuilder.java:26)\
 at
org.junit.runners.model.RunnerBuilder.safeRunnerForClass(RunnerBuilder.java:59)\
 at
org.junit.internal.requests.ClassRequest.getRunner(ClassRequest.java:26)\
 at
org.junit.internal.requests.FilterRequest.getRunner(FilterRequest.java:31)\
 at
com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:49)\
 at
com.intellij.rt.execution.junit.IdeaTestRunner\$Repeater.startRunnerWithArgs(IdeaTestRunner.java:47)\
 at
com.intellij.rt.execution.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:242)\
 at
com.intellij.rt.execution.junit.JUnitStarter.main(JUnitStarter.java:70)\
**Caused by: java.lang.IllegalStateException: SpringJUnit4ClassRunner
requires JUnit 4.12 or higher.**\
 at org.springframework.util.Assert.state(Assert.java:73)\
 at
org.springframework.test.context.junit4.SpringJUnit4ClassRunner.(SpringJUnit4ClassRunner.java:104)\
 … 15 more

**原因：JUnit包需要更高版本！**

**注意：各个jar包版本联系，避免冲突！**

 **错误日志需要认真分析！**

[相关链接1](https://blog.csdn.net/weixin_38771884/article/details/84136703)

[相关链接2](https://blog.csdn.net/guanwangzhe521/article/details/51470241)

### 4、主配置文件的分包配置

主配置文件中加入：

```xml
<import resource="applicationContextInjection.xml"/>
<import resource="applicationContextAnnotation"/>
```



part4 小结与练习
--------------------------------------------------------

### 1、 使用servlet技术开发用户登陆功能；

### 2、 在项目中加入Spring框架 

![关系图](https://github.com/ZephXu07/IMG/raw/master/%E4%BD%BF%E7%94%A8Spring%E6%94%B9%E9%80%A0Servlet%E9%A1%B9%E7%9B%AE%E5%AF%B9%E8%B1%A1%E5%85%B3%E7%B3%BB%E4%BE%9D%E8%B5%96%E5%9B%BE.png)

#### i. 将service、dao、dateSource交给Spring管理；

userDaoImpl中的`private ComboPooledDataSource dataSource`配置：

```java
 static {   
 	try {       
        //配置c3p0，连接数据库       
        dataSource = new ComboPooledDataSource();        
        dataSource.setDriverClass("com.mysql.cj.jdbc.Driver");                 
        dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai");        
        dataSource.setUser("root");        
        dataSource.setPassword("10709991");   
    } catch (PropertyVetoException e) {        
        e.printStackTrace();
}                          |
```

改为applicationContext.xml中：

```xml
 <!--配置dataSource-->
<bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"> 
     <property name="driverClass" value="com.mysql.cj.jdbc.Driver"/> 
     <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai"/>    
     <property name="user" value="root"/>    
     <property name="password" value="10709991"/>
 </bean>
```

还有dao, service中的配置

```xml
 <!--配置Dao-->
 <bean name="userDao"class="com.zephxu.dao.UserDaoImpl">
 	<property name="dataSource" ref="dataSource"/>
 </bean>
 <!--配置Service-->
 <bean name="userService" class="com.zephxu.service.UserServiceImpl">
 	<property name="userDao" ref="userDao"/>
 </bean>
```



**缺点：每一个请求都要new一个容器，而web项目中只需要一份，下一步提供解决方法。**

#### ii. 在web.xml中配置Spring监听器和读取配置文件[（SSM整合相关内容链接）](https://zephxu07.github.io/2019/10/15/SSM%E6%A1%86%E6%9E%B6%E6%95%B4%E5%90%88/#b-%E3%80%81%E6%B3%A8%E6%84%8F%EF%BC%9A)；

-   ServletContext类生命周期随web项目启动而创建，随web项目关闭而销毁。
-   ServletContextListener可以通过配置监听器来达到要求，在web项目创建时创建Spring容器，销毁时关闭Spring容器。

web.xml文件配置：

```xml
<!--配置监听器，在web项目启动时让Spring启动-->
<listener>    
	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class></listener>
<!--读取Spring的配置文件-->
<context-param>    
	<param-name>contextConfigLocation</param-name>    
	<param-value>classpath:applicationContext</param-value>
</context-param> 
```



Servlet类由

`ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext"); `

改为：

`WebApplicationContext wac = WebApplicationContextUtils.getWebApplicationContext(getServletContext());`

part5 Spring-aop 
--------------------------------------------------------

### 1、 aop思想介绍（面向切面编程）：将纵向重复代码，横向抽取解决，简称：横切 

![例图](https://github.com/ZephXu07/IMG/raw/master/aop%E6%80%9D%E6%83%B3%E6%A6%82%E5%BF%B5%E4%B8%BE%E4%BE%8B.png)

### 2、 Spring中的aop：无需我们自己写动态代理的代码，spring可以将容器中管理对象生成动态代理对象，前提是我们对他进行一些设置； 

### 3、 Spring-aop是基于动态代理的 – 优先选用JDKProxy动态代理；

[更加详细的动态代理](https://zephxu07.github.io/2019/10/02/%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86%E7%AC%94%E8%AE%B0/)

![example](https://github.com/ZephXu07/IMG/raw/master/Snipaste_2019-10-02_18-01-30.png)

#### a) Proxy动态代理：被代理的对象必须要实现接口；

#### b) Cglib动态代理：被代理的对象不能被final修饰，基于继承；

### 4、 Spring aop相关名词说明 ；

![conceptual
graphs](https://github.com/ZephXu07/IMG/raw/master/Snipaste_2019-10-02_18-07-38.png)

### 5、 Spring aop配置： 

#### a) 导包： 

##### i. 基本包； 

##### ii. spring-aspects和spring-aop ；

##### iii. aop联盟包 – aopalliance；

##### v. aop织入包 - aspectj.weaver；

#### b) 自定义通知，五种自定义通知类型：

##### i. before 前置通知：在目标方法前调用 

##### ii. after 最终通知（后置通知）：在目标方法后调用，无论是否出现异常都会调用，类似finally 

##### iii. afterReturning 成功通知（后置通知）：在目标方法后执行后，并且执行成功时调用，出现异常则不调用 

##### iv. afterThrowing 异常通知（后置通知）：在目标方法后执行后，并且出现异常调用，执行成功时则不调用 

##### v. around 环绕通知：需要我们手动调用目标方法，并且可以设置通知

```java
 public class MyAdvice {    
     //    before 前置通知    
     public void before() {       
         System.out.println("before");    
     }    
     //    after 最终通知（后置通知） 
     public void after() {        
         System.out.println("after");   
     }   
     //  afterReturning 成功通知（后置通知）    
     public void afterReturning() {        
         System.out.println("afterReturning");
     }    
     //    afterThrowing 异常通知（后置通知）    
     public void afterThrowing() { 
         System.out.println("afterThrowing");    
     }   
     //    around 环绕通知     
     public Object around(ProceedingJoinPoint pjp) throws Throwable {      
         System.out.println("around before"); 
         Object proceed  = pjp.proceed();        
         System.out.println("around after");        
         return proceed; 
     }
 } 
```



#### c) 配置applicationContext.xml：

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.springframework.org/schema/beans"       xmlns:aop="http://www.springframework.org/schema/aop"       xsi:schemaLocation="http://www.springframework.org/schema/beans        http://www.springframework.org/schema/beans/spring-beans-4.3.xsd            http://www.springframework.org/schema/aop              http://www.springframework.org/schema/aop/spring-aop-4.3.xsd">    
 <!--目标对象-->    
 <bean name="userService" class="com.zephxu.service.UserServiceImpl"/>    <!--   通知对象 -->    
 <bean name="myAdvice" class="com.zephxu.aop.MyAdvice"/>   
     <aop:config>        
     <!-- 切入点           expression：切入点表达式， 可以配置要增强的方法 
     单独针对此方法：public void com.zephxu.service.UserServiceImpl.save()           较大范围：* com.zephxu.service.*ServiceImpl.*(..)，此表达式可对public等权限的service下所有以ServiceImpl结尾的所有方法增强不管此方法的参数几何及何返回值
     id：唯一标识-->        
             <aop:pointcut id="servicePc" expression="execution(* com.zephxu.service.*ServiceImpl.*(..))"/>        
     <!--切面：通知 + 切入点        -->        
             <aop:aspect ref="myAdvice">
             <!--绑定通知对象-->            
             <!--通知类型-->            
             <!-- 前置通知 --> 
             <aop:before method="before" pointcut-ref="servicePc"/> 
             <!-- 最终通知（后置通知）           -->  
             <aop:after method="after" pointcut-ref="servicePc"/>
             <!-- 成功通知（后置通知）          -->     
             <aop:after-returning method=" afterReturning" pointcut-ref="servicePc"/>            <!--    异常通知（后置通知） -->            
             <aop:after-throwing method="afterThrowing" pointcut-ref="servicePc"/>            <!--    环绕通知          -->            
             <aop:around method="around" pointcut-ref="servicePc"/>        
             </aop:aspect>  
     </aop:config>
 </beans> 
```



#### d）测试及结果 

```java
@RunWith(SpringJUnit4ClassRunner.class)@ContextConfiguration("classpath:applicationContext.xml")
public class AopTest {   
	@Resource(name = "userService")    
	UserService us;    
	@Test    
	public void test2() {        
		us.delete();   
    }
}     
```



***结果：***

![result](https://github.com/ZephXu07/IMG/raw/master/RunningResult.png)

***测试异常：***

![testThrow](https://github.com/ZephXu07/IMG/raw/master/TestThrow.png)

![ThrowingResult](https://github.com/ZephXu07/IMG/raw/master/ThrowResult.png)

#### e）bug及原因：

***BUG:***

***Caused by:
org.springframework.beans.factory.parsing.BeanDefinitionParsingException:
Configuration problem: tag needs aspect bean reference via ‘ref’
attribute when declaring advices.\
Offending resource: class path resource [applicationContext.xml]***\
***Aspect: ref=’’***

***Reason：***

![reason](https://github.com/ZephXu07/IMG/raw/master/BugReason.png)

part6、Spring与Jdbc 
-----------------------------------------------------------------

### 1、 使用JdbcTemplate操作数据库；

-   导包：新增jdbc、tx

```java
 public class UserDaoImpl implements UserDao {    
 	private static ComboPooledDataSource dataSource;
 	static {        
 		try {            // 配置c3p0，连接数据库            
            dataSource = new ComboPooledDataSource();      
            dataSource.setDriverClass("com.mysql.cj.jdbc.Driver"); 
            dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai");            
            dataSource.setUser("root");            
            dataSource.setPassword("10709991");
        } catch (PropertyVetoException e) {            
        	e.printStackTrace();        
        }   
	}    
	@Override    
	public User selectUserById(Integer id) { 
        JdbcTemplate jt = new JdbcTemplate(dataSource);
        String sql = "select * from user where u_id = ?";        
        User user = jt.queryForObject(sql, new RowMapper<User>() {
            @Override            
            public User mapRow(ResultSet rs, int index) throws SQLException {           	User u = new User();
                u.setU_id(rs.getInt("u_id"));
                u.setU_username(rs.getString("u_username"));
                u.setU_password(rs.getString("u_password"));                
                return u;
            }        
		}, id);        
		return user;   
    }
}      
```

### 2、 JdbcTemplate的增删改查操作；

```java
@Override   
public List<User> selectAllUser() {       
    String sql = "select * from user";       
    List<User> userList = jt.query(sql, new RowMapper<User>() {           			@Override 
        public User mapRow(ResultSet rs, int index) throws SQLException {   
       		User u = new User();              
			u.setU_id(rs.getInt("u_id"));              
			u.setU_username(rs.getString("u_username"));     
            u.setU_password(rs.getString("u_password"));               
            return u;           
        }      
    });        
    return userList;  
}   
@Override   
public Integer selectUserCount() { 
    String sql = "select count(*) from user";       
    return jt.queryForObject(sql, Integer.class); 
}   
@Override   public void addUser(User user) {     
    String sql = "insert into user values(null, ?, ?)";   
    jt.update(sql, user.getU_username(), user.getU_username());  
}   
@Override 
public void deleteUser(Integer id) {       
    String sql = "delete from user where u_id = ?";       
    jt.update(sql, id);   
}   
@Override  
public void update(User user) {   
    String sql = "update user set u_username = ?, u_password = ? where u_id = ?" ;       
    jt.update(sql, user.getU_username(), user.getU_password(), user.getU_id()); 
}         
```

### 3、 让Spring容器管理JdbcTemplate；

```xml
 <!--依赖关系：dao -> jdbcTemplate ->  dataSource -->
 <!--    dataSource-->
 <bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">   	
 	<property name="driverClass" value="com.mysql.cj.jdbc.Driver"/> 
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai"/>   
    <property name="user" value="root"/> 
    <property name="password" value="10709991"/>
</bean>
<!--    jdbcTemplate-->
<bean name="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTe mplate">    
	<property name="dataSource" ref="dataSource"/>
</bean>
<!--dao-->
<bean name="userDao" class="com.zephxu.dao.UserDaoImpl">   
	<property name="jt" ref="jdbcTemplate"/>
</bean>
```



### 4、 继承JdbcDaoSupport甩开JdbcTemplat 

`public class UserDaoImpl extends JdbcDaoSupport implements UserDao { }`

```xml
<!--依赖关系：dao -> dataSource -->
<!--    dataSource-->    
<bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">           
	<property name="driverClass" value="com.mysql.cj.jdbc.Driver"/> 
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai"/>       
    <property name="user" value="root"/>          
    <property name="password" value="10709991"/> 
</bean> 
    <bean name="userDao" class="com.zephxu.dao.UserDaoImpl">  
    <property name="dataSource" ref="dataSource"/> 
</bean>      
```



### 5、 在Spring中读取配置文件

db.properties：

```properties
jdbc.driverClass=com.mysql.cj.jdbc.Driver
jdbc.jdbcUrl=jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai
jdbc.user=rootjdbc. password=10709991               
```

applicationContext.xml：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.springframework.org/schema/beans"       xmlns:context="http://www.springframework.org/schema/context"       xsi:schemaLocation="http://www.springframework.org/schema/beans       http://www.springframework.org/schema/beans/spring-beans.xsd        http://www.springframework.org/schema/context        http://www.springframework.org/schema/context/spring-context.xsd">   
<!--读取配置文件-->        
<context:property-placeholder location="db.properties"/>   
	<bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">      
    <property name="driverClass" value="${jdbc.driverClass}"/>        
    <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>        
    <property name="user" value="${jdbc.user}"/>     
    <property name="password" value="${jdbc.password}"/>  
</bean>
</beans>         
```



part7 Spring中的aop事务 
-----------------------------------------------------------------------------

### 1、事务相关知识 

#### a) 什么是事务： 

把多条数据库操作捆绑到一起执行，要么都成功，要么都失败；

#### b) 事务的原则ACID：

i.
原子性：事务包含的所有操作，要么全部成功，要么全部失败回滚，成功全部应用到数据库，失败不能对数据库有任何影响；

ii.
一致性：事务在执行前和执行后必须一致；例如A和B一共有100块钱，无论A、B之间如何转账，他们的钱始终相加都是100；

iii.
隔离性：多用户并发访问同一张表时，数据库为每一个用户开启新的事务，该事务不能被其他事务所影响，相互有隔离；

iv.
持久性：一个事务一旦提交，则对数据库中数据的改变是永久的，即便系统故障也不会丢失；

#### c) 并发可能引起的问题：

i. 脏读：一个事务读取到另一个事务未提交的数据；

ii.
不可重复读：一个事务读取到另一个事务已提交(Update操作)的数据，导致前后读取不一致；

iii.
幻读（虚读）：一个事务中读取到别的事务插入(Insert操作)的数据，导致前后读取不一致；

#### d) 事务的隔离级别：根据实际情况选择；

i. Serializable串行化：可避免脏读、不可重复读和幻读；

ii. Repeatable read可重复读：可避免脏读、不可重复读；（MySql默认值）

ii. Read committed读已提交：可避免脏读；

iv. Read uncommitted读未提交：任何情况都无法保证；

#### e) [更加详细的事务介绍](https://www.cnblogs.com/xdp-gacl/p/3984001.html)

### 2、Spring-aop事务-搭建环境 

#### a) 事务基本操作：打开事务、提交事务、回滚事务；

#### b) Spring中利用接口来管理不同框架的事务操作；

i.
通过实现PlatformTransactionManager接口支持不同的框架完成各自的事务处理；

ii. 为不同平台提供对应的事务管理器的实现：

JDBC&Mybatis：DataSourceTransactionManager；

### 3、Spring-aop事务通过配置事务的隔离级别、事务传播行为、是否只读来操作；

#### i. 隔离级别：串行化、可重复读、读已提交、读未提交；

#### ii. 是否只读：

  1. true：不可改变数据库中的数据，查询操作推荐，

  2. false：可以改变数据库数据；

#### iii. 事务传播行为：事务方法嵌套调用的规则：

 xService.x(); -\> yService.y();

 1.
REQUIRED：如果当前没有事务，就创建一个新事务，如果当前存在事务，就加入该事务，***该设置是最常用的设置***；

  2. REQUIRES\_NEW：创建新事务，无论当前存不存在事务，都创建新事务；

 3.
SUPPORTS：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就以非事务执行；

 4.
NOT\_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起（暂停）；

 5.
MANDATORY：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就抛出异常；

  6. NEVER：以非事务方式执行，如果当前存在事务，则抛出异常；

 7.
NESTED：如果当前存在事务，则在嵌套事务内执行（y开启新的事务）。如果当前没有事务，则执行与REQUIRED类似的操作。

### 4、Spring-aop事务-– 从麻烦的事务代码中走出之xml配置版aop事务； 

#### a) 使用经典的转账案例进行测试，准备数据：bean、service、dao；

```java
public void transferAccounts() { 
    //转账        
    //A - 50         
    accountDao.subMoney(1, 50d);      
    //异常        
    int value = 1 / 0;      
    //B + 50        
    accountDao.addMoney(2, 50d);   
}    
```



#### b) 使用事务需要额外导入tx包和tx约束；

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.springframework.org/schema/beans"       xmlns:context="http://www.springframework.org/schema/context"       xmlns:tx="http://www.springframework.org/schema/tx" xmlns:aop="http://www.springframework.org/schema/aop"      
xsi:schemaLocation="http://www.springframework.org/schema/beans       http://www.springframework.org/schema/beans/spring-beans.xsd        http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd 
http://www.springframework.org/schema/tx        
http://www.springframework.org/schema/tx/spring-tx.xsd  
http://www.springframework.org/schema/aop        
http://www.springframework.org/schema/aop/spring-aop.xsd">
</beans>     
```



#### c) 配置事务核心管理器: DataSourceTransactionManager； 

```xml
<!--配置事务核心管理器，不同平台不一样-->
<bean name="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager"> 
	<property name="dataSource" ref="dataSource"/>
</bean>      
```



#### d) 配置事务通知 tx:Advice；

```xml
 <!--配置事务通知    -->    
 <tx:advice id="txAdvice" transaction-manager="transactionManager">        
     <tx:attributes>                 
         <tx:method name="transferAccounts" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>           
         <!--isolation隔离级别，propagation传播行为，read-only="false"为有对数据库进行修改-->    
         <tx:method name="save*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>            
         <tx:method name="delete*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>       
         <tx:method name="update*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>           
         <tx:method name="select*" isolation="DEFAULT" propagation="REQUIRED" read-only="true"/>
         <!--没有对数据库进行修改-->    
     </tx:attributes>    
 </tx:advice>    
```



#### e) 配置aop；

```xml
<!--配置aop--><aop:config>   
<aop:pointcut id="txPc" expression="execution(* com.zephxu.service.*ServiceImpl.*(.. ))"/>   
<!--切入点-->    
<aop:advisor advice-ref="txAdvice" pointcut-ref="txPc"/>  
<!--通知-- >
</aop:config>      
```



**出现异常`int value = 1 / 0;`时因为加入事务管理，自动事务回滚。**

![存在事务管理](https://github.com/ZephXu07/IMG/raw/master/exist.png)

***若没有事务管理，则前者转出成功，但后者并没有收到。***

![不存在事务管理](https://github.com/ZephXu07/IMG/raw/master/Simple.png)

#### f) BUG：

Caused by: org.springframework.beans.factory.BeanCreationException:
Error creating bean with name ‘dataSource’ defined in class path
resource [applicationContext.xml]: Initialization of bean failed; nested
exception is java.lang.IllegalArgumentException: Pointcut is not
well-formed: expecting ‘name pattern’ at character position 45\
***execution(\*com.zephxu.service.\*ServiceImpl.\\*(.. ))\***

***原因：***

`<aop:pointcut id="txPc" expression="execution(* com.zephxu.service.*ServiceImpl.*(..))"/>   `

**在 \* 与com之间需要空格！**

### 5、Spring-aop事务 – 从麻烦的事务代码中走出之注解版aop事务。 

**配置事务通知 tx:Advice**与**配置aop**更改为：

`<!--开启注解事务--><tx:annotation-driven/>  `

`@Transactional(isolation = Isolation.DEFAULT, propagation = Propagation.REQUIRED, readOnly = false)   `

**注解在方法上就此方法开启事务，也可以将注解放在此类上，则此类所有方法都开启事务，若某方法有特别的事务配置仅需在那方法上设置新的注解。**

**BUG：**

**Error creating bean with name ‘dataSource’ defined in class path
resource [applicationContext2.xml]: Initialization of bean failed;
nested exception is java.lang.NoSuchMethodError:
org.springframework.core.annotation.AnnotationUtils.isCandidateClass(Ljava/lang/Class;Ljava/lang/Class;)Z**

**原因：导包缺少，仔细与视频中对比，发现少了spring-aspects，com.springsource.org.aspectj.weaver，com.springsource.org.aopalliance三个jar包，且[Spring
Core](https://mvnrepository.com/artifact/org.springframework/spring-core)需要最新！**

**强烈建议：Spring版本通过maven版本锁定，[相关链接](https://blog.csdn.net/qq_37393900/article/details/80240015)**

![版本锁定](https://github.com/ZephXu07/IMG/raw/master/SpringVersion.png)

![跟随版本](https://github.com/ZephXu07/IMG/raw/master/FollowSpringVersion.png)

part8、Spring整合Mybatis加入事务操作数据库 
--------------------------------------------------------------------------------------------------------------------------------------

### 1、 整合Mybatis 

#### a) 导包： 

i. Spring：基本包、aop、aspects、jdbc、tx、test；

ii. Mybatis：mybatis

iii. 整合包：mybatis-spring

iv. 三方包：

1.  aopalliance

2.  aspectj.weaver

3.  c3p0

4.  mchange-commons-java

5.  mysql-connector-java

#### b) 创建项目结构(package)：bean、service、mapper、test； 

![项目结构](https://github.com/ZephXu07/IMG/raw/master/ssm_spring_mybatis_txProjectStructure.png)

#### c) 创建配置文件：sqlMapperConfig、applicaitonContext 

sqlMapperConfig：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC"-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>        
<typeAliases>             
	<package name="com.zephxu.bean"/>     
</typeAliases>
</configuration> 
```



applicaitonContext：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.springframework.org/schema/beans"    
xmlns:context="http://www.springframework.org/schema/context"       xmlns:tx="http://www.springframework.org/schema/tx" xmlns:aop="http://www.springframework.org/schema/aop" xsi:schemaLocation="http://www.springframework.org/schema/beans       http://www.springframework.org/schema/beans/spring-beans.xsd        http://www.springframework.org/schema/contexthttp://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx        http://www.springframework.org/schema/tx/spring-tx.xsd http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd"> 
<!--数据源-->    
<context:property-placeholder location="db.properties"/>
<!--读取配置文件-->   
<bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"><!--配置DataSource-->        
<property name="driverClass" value="${jdbc.driverClass}"/>       
<property name="jdbcUrl" value="${jdbc.jdbcUrl}"/> 
<property name="user" value="${jdbc.user}"/> 
<property name="password" value="${jdbc.password}"/>   
</bean>    
<!--mybatis--> 
<bean name="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<property name="dataSource" ref="dataSource"/>        <property name="configLocation" value="classpath:sqlMapConfig.xml"/> 
</bean>    
<!--mapper工厂-->   
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">        
    <property name="basePackage" value="com.zephxu.mapper"/> 
</bean>   
<!--service-->   
<bean name="accountService" class="com.zephxu.service.AccountServiceImpl"/></beans>                  
```



### 2、 创建测试用例：使用Mapper扫描开发，转账； 

AccountMapper.xml：

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE mapper        PUBLIC"-//mybatis.org//DTD Mapper 3.0//EN"        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zephxu.mapper.AccountMapper">
   <update id="transferOutMoney" parameterType="Account">        
       update account set money = money - #{transferMoney} where id = #{id}   
   </update>    
   <update id="transferInMoney" parameterType="Account"> 
   updat e account set money = money + #{transferMoney} where id = #{id}    	
   </update>
</mapper>                   
```



### 3、 在service中加入事务：利用Spring-aop事务解决转账异常问题； 

xml：

```xml
<!--事务核心管理器-->    
<bean name="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">        <property name="dataSource" ref="dataSource"/>   
</bean>
<!--    事务通知-->  
<tx:advice id="txAdvice" transaction-manager="transactionManager">        <tx:attributes>            
<tx:method name="update*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>        
</tx:attributes> 
</tx:advice>
<!--    aop-->   
<aop:config>        
<aop:pointcut id="txPc" expression="execution(* com.zephxu.service.*ServiceImpl.*(..))"/> 
<aop:advisor advice-ref="txAdvice" pointcut-ref="txPc"/>  
</aop:config> 
```



注解：[如上](#aop)

**BUG：Invalid bound statement (not found):
com.zephxu.mapper.AccountMapper.transferOutMoney**

**原因：maven项目，xml文件不在resource目录下，而在java目录下，需要在pom.xml中加上**

```xml
  <build>   
  <resources>        
  	<resource>   
  		<directory>src/main/java</directory> 
        <includes> 
        	<include>**/*.xml</include>   
        </includes>
     </resource>
   </resources>
   </build>                     
```



[解决方法来源](https://blog.csdn.net/ccoran/article/details/85044096)

part9、未完待续…… 
-----------------------------------------------------------