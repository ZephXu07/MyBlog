---
title: MyBatis笔记
date: 2020-01-23 23:18:43
tags: [笔记, mybatis, ssm, java]
---

MyBatis笔记
===========

SSM框架系列之一 MyBatis
-----------------------------------------------------------------------------

what
--------------------

 MyBatis 本是apache的一个开源项目iBatis, 2010年由apache software foundation 迁移到了google code，并且改名为MyBatis 。2013年11月迁移到Github。

 MyBatis是支持定制化 SQL、存储过程以及高级映射的优秀的持久层框架。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以对配置和原生Map使用简单的 XML 或注解，将接口和 Java 的 POJOs(Plain Old Java Objects,普通的 Java对象)映射成数据库中的记录。（专业语言，抄的……）

 总而言之MyBatis是一个轻量级简化数据库操作的框架。

<!--more-->

why using MyBatis
-----------------------------------------------------------

*解决JDBC存在的问题和简化数据库操作*：

- 可以通过主配置文件配置连接池解决频繁创建、释放数据库连接造成的性能影响

  ```xml
  <!--  使用jdbc的事务          -->
  <transactionManager type="JDBC"/>
  	<dataSource type="POOLED">
  		<property name="driver" value="com.mysql.cj.jdbc.Driver"/>
  		<property name="url" value="jdbc:mysql://localhost:3306/ssm_mybatis?serverTimezone=Asia/Shanghai"/>
          <property name="username" value="root"/>
          <property name="password" value="10709991"/>
      </dataSource>
  ```

- 动态SQL解决JDBC中硬编码问题

- -   Where条件改变
  -   占位符位置变化
  -   mapper.xml 文件书写

- 可通过包装类方便的获取数据库查询结果集对象

- 使Dao层业务逻辑和数据库访问分离更易维护和测试

learn what
--------------------------------------

-   了解MyBatis架构；
-   掌握MyBatis框架搭建、配置
-   使用MyBatis完成对数据库的增、删、改、查操作
-   掌握Mapper代理开发
-   掌握输入和输出映射
-   掌握多表关联查询
-   掌握动态SQL编写SQL语句
-   使用MyBatis Generator工具快速生成Bean、Interface、mapper.xml
-   掌握MyBatis+Spring开发(需要部分Spring知识)

开始学习MyBatis 框架
====================================================================

part1 MyBatis架构图：
-----------------------------------------------------------------------

![架构图](https://github.com/ZephXu07/IMG/raw/master/MyBatis%E6%9E%B6%E6%9E%84%E5%9B%BE.png)

-   顶部算入口
-   SqlMapConfig.xml主配置文件
-   Mapper.xml对应一张表，几张对应几个xml文件
-   SqlSessionFactory是上述配置文件通过SqlSessionFactoryBuilder创建的
-   实线是初步学习关注的，虚线为后续深入学习需要关注的

part2 HelloMyBatis：搭建MyBatis HelloWorld项目
--------------------------------------------------------------------------------------------------------------------------------------------------

1、 下载MyBatis、创建项目、导包；

2、 创建测试用例，测试数据库、测试Bean对象；

3、 创建sqlMapConfig.xml主配置文件；

-   导入主配置文件头：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
```



4、 创建Mapper.xml映射文件；

-   导入Mapper文件头：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
```

5、 导入约束；

part3 使用MyBatis对表进行增、删、改、查操作
-----------------------------------------------------------------------------------------------------------------------------------------

**SqlSession对象对数据库有增加、修改、删除都需要commit!**

1、 通过ID去查询一个用户

![1](https://github.com/ZephXu07/IMG/raw/master/mybatis.png)

- 需要一个UserMapper接口，方法名，返回值，参数的需要一致。

```java
//读取配置文件
   String resource = "sqlMapConfig.xml";
   InputStream is = Resources.getResourceAsStream(resource);
    
    //需要sqlSessionFactoryBuilder
    SqlSessionFactoryBuilder saab = new SqlSessionFactoryBuilder();
       
    //创建sqlSessionFactory
    SqlSessionFactory ssf = saab.build(is);
       
    //生产一个sqlSession
    SqlSession ss = ssf.openSession();
       
    //操作数据库
    //参1：sql，参2：sql语句中参数
    User user = ss.selectOne("com.zephxu.bean.UserMapper.selectUserById", 1);
```

```xml
<select id="selectUserById" parameterType="Integer" resultType="com.zephxu.bean.User">
        select * from user where u_id = #{id}<!--mapper中间为sql语句-->
</select>
```

-   \#{id}占位符，即?
-   log4j.properties文件应只有一份且存在于src\\main\\resources\\下且不在其他子文件下。

2、 通过用户名模糊查找匹配的用户列表

```java
List<User> userList = ss.selectList("com.zephxu.bean.UserMapper.selectUserByName", "c");
```

```xml
<select id="selectUserByName" parameterType="String" resultType="com.zephxu.bean.User"><!--其他同上-->
<!--         select * from user where u_username like '%${value}%'-->
        select * from user where u_username like "%"#{name}"%"
</select>
```

-   \${value}：字符串拼接符，容易导致sql注入，如1 = 1，避免使用。
-   \#{value}：占位符，预处理，即PreparedStatement，可以防止sql注入，尽量使用。

3、 完成添加用户

```java
User user = new User(50, "xz", "1079991", "1", new Date(), 2);
ss.insert("com.zephxu.bean.UserMapper.insertUser", user);
```

-   BUG：Cannot add or update a child row: a foreign key constraint fails (`ssm_mybatis`.`user`, CONSTRAINT `FK_user_cid` FOREIGN KEY (`u_cid`) REFERENCES `country` (`c_id`))
    -   这个表某字段与其他表某字段有外键连接时，此时数据应为另一个表已存在数据。

```xml
<insert id="insertUser" parameterType="com.zephxu.bean.User">
        INSERT into user values (#{u_id}, #{u_username}, #{u_password}, #{u_sex}, #{u_createTime}, #{u_cid})
</insert>
```

4、 修改用户

```java
ss.update("com.zephxu.bean.UserMapper.updateUser", user);
```

```xml
<update id="updateUser" parameterType="com.zephxu.bean.User">
        update user set u_username = #{u_username} where u_id = #{u_id}
</update>
```

-   同上

5、 根据id删除用户

```java
ss.delete("com.zephxu.bean.UserMapper.deleteUserById", 90);
```

```xml
<delete id="deleteUserById" parameterType="Integer">
        delete from user where u_id = #{u_id}
</delete>
```

-   同上

6、 使用MyBatis 开发Dao层并测试；

7、 小结1：Jdbc与MyBatis开发的区别(MyBatis的优点)，回顾MyBatis开发流程；

part4 **MyBatis Mapper动态代理开发4+1 (4原则+1注意)：**
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

1、 接口方法名需要与mapper.xml的要调用的sql语句的id一致；

2、 接口的形参类型需要与mapper.xml parameterType一致；

3、 接口的返回值需要与mapper.xml resultType一致；

4、 mapper.xml中namespace要与接口的全包名一致；

5、 注意mapper动态代理开发中，根据返回值类型来自动选择；

![4](https://github.com/ZephXu07/IMG/raw/master/mybatis4.png)

![5](https://github.com/ZephXu07/IMG/raw/master/mybatis5.png)

-   上两图对应1-4点

```java
@Test
    public void test1() throws IOException {
        //读取配置文件
        String resource = "sqlMapConfig.xml";
        InputStream is = Resources.getResourceAsStream(resource);
        //创建sqlSessionFactory
        SqlSessionFactory ssf = new SqlSessionFactoryBuilder().build(is);
        //生产一个sqlSession
        SqlSession ss = ssf.openSession();
        UserMapper userMapper = ss.getMapper(UserMapper.class);
        User user = userMapper.selectUserById(99);
        System.out.println(user);
    }
```

-   倒数三行是动态代理原理，获得UserMapper唯一的模板去创建一个对象，但现在如何从未实现的UserMapper接口和一个相关的UserMapper.xml文件创建未知，可能Mybatis中已有具体方法从接口及相关xml文件生成具有具体实现方法的代理类。

```java
User user = ss.selectOne("com.zephxu.mapper.UserMapper.selectUserById", 1);
```

```java
userMapper.insertUser(user);
   user.setU_username("王yang");
   userMapper.updateUserById(user);
   List<User> userList = userMapper.selectUserByName("王");
   for (User u:userList) {
   	System.out.println(u);
   }
   userMapper.deleteUserById(88);
```

相比之下虽代码多了，但其实更加好理解，一个UserMapper的对象，其有各种各样的方法，只需要调用，而不需要通过参数方式”com.zephxu.mapper.UserMapper.selectUserById”进行调用。

part5 主配置文件SqlMapConfig.xml说明：（注意顺序）
--------------------------------------------------------------------------------------------------------------------------------------------------------------

**（加粗为前期学习重点）**

1、 **properties（读取配置文件）**

- 不使用时：

  ```xml
  <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
  <property name="url" value="jdbc:mysql://localhost:3306/ssm_mybatis?serverTimezone=Asia/Shanghai"/>
  <property name="username" value="root"/>
  <property name="password" value="10709991"/>
  ```

- 使用时将包内的映射器接口实现全部注册为映射器：

  ![00](https://github.com/ZephXu07/IMG/raw/master/UC%E6%88%AA%E5%9B%BE20190918194909.png)

  ```xml
  <properties resource="db.properties"/>
  <property name="driver" value="${jdbc.driver}"/>
  <property name="url" value="${jdbc.url}"/>
  <property name="username" value="${jdbc.username}"/>
  <property name="password" value="${jdbc.password}"/>
  ```

  -   如果属性在不只一个地方进行了配置，那么 MyBatis 将按照下面的顺序来加载：
      -   在 properties 元素体内指定的属性首先被读取。
  -   然后根据 properties 元素中的 resource 属性读取类路径下属性文件或根据 url 属性指定的路径读取属性文件，并覆盖已读取的同名属性。
      -   最后读取作为方法参数传递的属性，并覆盖已读取的同名属性。

2、 settings（全局配置参数）

3、 **typeAliases（类型别名）**

![5.3](https://github.com/ZephXu07/IMG/raw/master/mybatis.5.3.png)

- 别名可用于此处，省略包名。

- `<typeAliases></typeAliases>`中有两种用法：

  1.  单独： `<typeAlias type="com.zephxu.bean.User" alias="User"/>`
  2.  （推荐）包：`<package name="com.zephxu.bean"/>`

  - `resultType="User"`

  - `resultType="user"`

  - 大小写均可。

     BUG：

    -   Cause: org.apache.ibatis.builder.BuilderException: Error creating document instance. Cause: org.xml.sax.SAXParseException; lineNumber: 57; columnNumber: 17; 元素类型为 “configuration” 的内容必须匹配 “(properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,objectWrapperFactory?,reflectorFactory?,plugins?,environments?,databaseIdProvider?,mappers?)”。
    -   原因：`<configuration>`标签中的小标签需要符合一定顺序：
    -   ==properties–settings–typeAliases–typeHandlers–objectFactory–objectWrapperFactory–reflectorFactory–plugins–environments–databaseIdProvider–mappers==

4、 typeHandlers（类型处理器）

5、 objectFactory（对象工厂）

6、 plugins（插件）

7、 environments（环境集合属性对象，与Spring框架整合后Say Good Bye）

 a) environment（环境子属性对象）

 b) transactionManager（事务管理）

 c) dataSource（数据源）

8、 **mappers（配置映射器位置）**(1-3单独，4包)

 （1）使用相对于类路径的资源引用

`<mapper resource="mapper/UserMapper.xml"/>`

 （2）使用完全限定资源定位符（URL）

```xml
<mapper url="file:///D:\IDEAWorkSpace\ssm_MyBatis\src\main\resources\mapper\UserMapper.xml"/> 
<!--"file:///" + 绝对路径-->
```

 （3）使用映射器接口实现类的完全限定类名

 `<mapper class="com.zephxu.mapper.UserMapper"/>`

 **注意：把同名xml文件复制到接口同个包下，且在resource目录下的包名需要完全一致，编译后在target目录下才会在同一包内。[或者此BUG对应的解决方法](https://zephxu07.github.io/2019/09/27/Spring-Learning-Notes/#3%E3%80%81-%E5%9C%A8service%E4%B8%AD%E5%8A%A0%E5%85%A5%E4%BA%8B%E5%8A%A1%EF%BC%9A%E5%88%A9%E7%94%A8Spring-aop%E4%BA%8B%E5%8A%A1%E8%A7%A3%E5%86%B3%E8%BD%AC%E8%B4%A6%E5%BC%82%E5%B8%B8%E9%97%AE%E9%A2%98%EF%BC%9B)**

![5.8.3](https://github.com/ZephXu07/IMG/raw/master/mybatis.5.8.3.png)

 （4）将包内的映射器接口实现全部注册为映射器

 **规则同3，但是为一整个包为单位**

part6 MyBatis输入和输出映射
-----------------------------------------------------------------------------------------

1、 输入映射parameterType；

 a) 基本类型；

 b) 自定义对象；

 c) 自定义包装类：本对象之外额外的信息。

2、 输出映射resultType、resultMap；**不能同时使用！！！**

 a) resultType：bean包中类中属性名需完全一致才能自动映射。

 i. 基本类型；

 ii. 自定义对象；

 iii. 集合；

**BUG** : `select count(*) from user`

**count后面没有空格！！！**

b) resultMap；

 i. bean对象字段与数据表字段不匹配，如下；

```java
private Integer id;
private String name;
private String capital;
```

![6.b.i](https://github.com/ZephXu07/IMG/raw/master/mybatis.6.b.i.png)

![6.i.1](https://github.com/ZephXu07/IMG/raw/master/mybatis.6.b.i.1.png)

**注意：单表查询时`<resultMap>`中不能用id标签，需要用reslut标签，特别是java/com/zephxu/mapper中的mapper.xml文件**

 ii. 自定义包装类；

 iii. 关联查询；

part7 MyBatis关联查询
-----------------------------------------------------------------------

1.  一对一；
2.  一对多；
    -   **多表查询中resultMap中建议主键时用id，而其他字段使用result，提升性能。**
    -   **单表查询中bean对象字段与数据表字段匹配时可以不用映射，但多表关联查询需要。**

![7.1](https://github.com/ZephXu07/IMG/raw/master/mybatis.7.1.png)

1 . 一对一：

```xml
<resultMap id="uservolist" type="UserVo">
        <id property="u_id" column="u_id"/>
        <result property="u_username" column="u_username"/>
        <result property="u_sex" column="u_sex"/>
    <!--多表查询中resultMap中建议主键时用id，而其他字段使用result-->
    <!--一对一的关系，上为主表，下为辅表，使用<association>标签-->
        <association property="country" javaType="Country">
            <id property="id" column="c_id"/>
            <!--单表查询中bean对象字段与数据表字段匹配时可以不用映射，但多表关联查询需要-->
            <result property="name" column="c_countryname"/>
            <result property="capital" column="c_capital"/>
            <!--同上-->
        </association>
</resultMap>
<select id="selectAllUserVo" resultMap="uservolist">
        select
            u.`u_id`, u.`u_username`, u.`u_sex`,c.`c_id`, c.`c_countryname` , c.`c_capital`
                from user u
                    left join country c
                        on u.`u_cid`=c.`c_id`
</select>
```

2.一对多

```xml
<resultMap id="countryVo" type="CountryVo">
    	<!--id、result使用同上-->
        <id property="id" column="c_id"/>
        <result property="name" column="c_countryname"/>
        <result property="capital" column="c_capital"/>
        <!--一对多关系使用collection-->
        <collection property="userList" <!--一对多中的多对应的泛型集合--> ofType="User"<!--泛型集合中的数据类型-->
            <id property="u_id" column="u_id"/>
            <result property="u_username" column="u_username"/>
    		<!--id、result使用同上-->
        </collection>
</resultMap>
<select id="selectAllCountryVo" resultMap="countryVo">
        select
            c.`c_id`, c.`c_countryname`, c.`c_capital`,
                u.`u_id`, u.`u_username`
                    from country c
                        left join
                            user u on
                                u.`u_cid`=c.`c_id`
</select>
```

part8MyBatis动态sql：更方便的拼接sql语句！
--------------------------------------------------------------------------------------------------------------------------------------

1、 if标签 - 多条件查询，获取用户列表；

```xml
<select id="selectUserListByUser" parameterType="User" resultType="User">
        select * from user
            where
                <if test="u_sex != null and u_sex != ''">
                    u_sex = #{u_sex}
                </if>
                <if test="u_username != null and u_username != ''">
                    and u_username like "%"#{u_username}"%"
                </if>
                <if test="u_cid != null">
                    and u_cid = #{u_cid}
                </if>
</select>
```

**注意：可能因为某个if出现sql语句错误，如**

 **`select * from user where and u_username like "%"?"%"`**

解决方法如2。

2、 where标签 - 解决if标签拼接字符串AND符号问题；

```xml
<select id="selectUserListByUser" parameterType="User" resultType="User">
        select * from user
            <where>
                <if test="u_sex != null and u_sex != ''">
                    u_sex = #{u_sex}
                </if>
                <if test="u_username != null and u_username != ''">
                    and u_username like "%"#{u_username}"%"
                </if>
                <if test="u_cid != null">
                    and u_cid = #{u_cid}
                </if>
        	</where><!--<where>标签可智能去除开头的and符号-->
</select>
```

3、 trim标签 - 定制where标签的规则

-   `<trim prefix="WHERE" prefixOverrides="AND">` 代替 `<where>`

-   prefix（suffix）替换前缀的where ，prefixOverrides（suffixOverrides）自动去掉开头的and，此外还有其他如下：

![0](https://github.com/ZephXu07/IMG/raw/master/Snipaste_2019-09-22_18-02-01_%E4%B8%AD%E5%9B%BD%E6%A0%87%E5%87%86%E6%97%B6%E9%97%B4_351ep18xu.png)

![3](https://github.com/ZephXu07/IMG/raw/master/Snipaste_2019-09-22_18-02-44_%E4%B8%AD%E5%9B%BD%E6%A0%87%E5%87%86%E6%97%B6%E9%97%B4_45ep18xu.png)

4、 set标签 - 解决更新数据表时字符串拼接逗号”,”问题；

```xml
<update id="updateSetUser" parameterType="User">
        update user
            <set>
                <if test="u_username != null and u_username != ''">
                    u_username = #{u_username},
                </if>
                <if test="u_password != null and u_password != ''">
                    u_password = #{u_password},
                </if>
                <if test="u_sex != null and u_sex != ''">
                    u_sex = #{u_sex}
                </if>
            </set>
                where u_id = #{u_id}
</update>
```

**`<set>`标签代替set，来处理`<if>`标签可能由于’,’造成的sql语句错误，且’,’可放置前面或后面，不似`<where>`标签只能处理前缀and！**

5、 foreach标签 – 如果需要使用IN查询多条相同数据，可以使用foreach遍历；

```xml
<select id="selectUserListByIds" resultType="User">
        select * from user where u_id in (1, 7, 18, 99);
</select>
```

SQL语句如上，使用`<foreach>`标签后如下：

```xml
<select id="selectUserListByIds" resultType="User">
        select *
            from user
                where u_id in <!--(1, 7, 18, 99);-->
                    <foreach collection="array" item="id" open="(" close=")" separator=",">
                    <!--使用标签后拼接为 "(1,7,18,99)" -->
                        #{id}
                    </foreach>
</select>
```

- `List<User> selectUserListByIds(Integer[] integers);`

   **参数为`Integer[] integers` 则`<collecction>`参数为”array”。**

- `List<User> selectUserListByIdList(List<Integer> idList);`

   **参数为`List<Integer> idList`则`<collection>`参数为”list”。**

- `List<User> selectUserListByUserVo(UserVo uv);`

   **参数`UserVo uv`则`<collection>`参数为包装类中的属性”idList”。**

  ![包装类信息](https://github.com/ZephXu07/IMG/raw/master/Snipaste_2019-09-24_16-55-10.png)

6、 sql标签 – 可以提取重复sql语句片段；

-   定义：

```xml
<sql id="mySelect">
        select * from user
</sql>
```

-   使用：

```xml
<include refid="mySelect"/>
```

part9 MyBatis Generator（MBG）：
---------------------------------------------------------------------------------------------------------

-   作用：根据数据库表自动生成Bean对象、Java接口及SqlMapper.xml配置文件；

-   [官方文档](http://www.mybatis.org/generator/)

-   [下载地址](https://github.com/mybatis/generator/releases)

1、 搭建MBG项目；

a) 下载MBG核心包；

b) 创建java项目；

c) 从官方文档获取配置表、实例代码；

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <!--<classPathEntry location="/Program Files/IBM/SQLLIB/java/db2java.zip" />-->
	<!--配置数据库的包，maven已导入，注释掉-->
    <context id="MyGenarator" targetRuntime="MyBatis3">
        <commentGenerator>
            <property name="suppressAllComments" value="true"/>
            <!--取消注释，当为true-->
            <property name="suppressDate" value="true"/>
            <!--取消时间戳，当为true-->
        </commentGenerator>
        
        <!--数据库连接信息-->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/ssm_mybatis?serverTimezone=Asia/Shanghai"
                        userId="root"
                        password="10709991">
        </jdbcConnection>

        <!--java JDBC数据类型转换，具体看https://mybatis.org/generator/configreference/javaTypeResolver.html-->
        <javaTypeResolver >
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>
<!--重点：javaModelGenerator Bean配置
			targetPackage：输入包名，输出路径
			targetProject：输出项目位置，相对路径，不需要写项目名，从src下开始-->
        <javaModelGenerator targetPackage="com.zephxu.bean" targetProject="src\main\java">
            <property name="enableSubPackages" value="false" />
            <!--是否开启子包名称，即是否在包名后边加scheme名称-->
            <property name="trimStrings" value="false" />
            <!--在Set中加入.trim-->
        </javaModelGenerator>

        <!--mappper.xml文件配置-->
        <sqlMapGenerator targetPackage="com.zephxu.mapper"  targetProject="src\main\java">
            <!--targetPackage，targetProject同上-->
            <property name="enableSubPackages" value="false" />
        </sqlMapGenerator>

        <!--java接口配置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.zephxu.mapper"  targetProject="src\main\java">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>

        <!--数据库：根据数据库中的表来生成-->
   <!--     <table schema="DB2ADMIN" tableName="ALLTYPES" domainObjectName="Customer" >
            <property name="useActualColumnNames" value="true"/>
            <generatedKey column="ID" sqlStatement="DB2" identity="true" />
            <columnOverride column="DATE_FIELD" property="startDate" />
            <ignoreColumn column="FRED" />
            <columnOverride column="LONG_VARCHAR_FIELD" jdbcType="VARCHAR" />
        </table> -->
        <!--过于复杂，简单如下-->
        <table tableName="user"/>
        <table tableName="country"/>
    </context>
</generatorConfiguration>
```

上述标签中在MYSQL中trim用法：

-   **重要知识点都在上面xml文档的注释中！**

d) 导入依赖包；

![依赖包](https://github.com/ZephXu07/IMG/raw/master/Snipaste_2019-09-25_19-12-48_%E4%B8%AD%E5%9B%BD%E6%A0%87%E5%87%86%E6%97%B6%E9%97%B4_334ep19xu.png)

- - git使用出现BUG：\*\*error: failed to push some refs to……

  - **解决方法：git pull –rebase origin master**

     **git push -u origin master**

  - 详解：

  [bug详解]: https://blog.csdn.net/MBuger/article/details/70197532(https://blog.csdn.net/MBuger/article/details/70197532)

2、 MBG配置以及根据数据库表生成所需文件（Bean、Interface、Mapper.xml）；

3、 使用自动生成的文件操作数据库：根据生成的Mapper类、UserExample类中特有的属性或方法去操作数据库，具体看方法。

part10、Mybatis + Spring 整合开发
---------------------------------------------------------------------------------------------------------

### 1、目的：

a) 使用Spring容器用单例模式管理Mybatis的sqlSessionFactory；

b) 使用Spring管理连接池、数据源等；

c) 将Dao/Mapper动态代理对象注入到Spring容器中，使用时直接获取；

### 2、 Mybatis和Spring框架整合；

a) 导入所需的包；

b) 创建Mybatis主配置文件sqlMapConfig.xml；

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--配置别名-->
    <typeAliases>
        <package name="com.zephxu.bean"/>
    </typeAliases>
</configuration>
```

c) 创建Spring主配置文件applicationContext.xml (以下是spring框架xml的头，需要导入约束)；

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
<!--数据源-->
    <context:property-placeholder location="db.properties"/><!--读取配置文件-->
    <bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"><!--配置DataSource-->
        <property name="driverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>
        <property name="user" value="${jdbc.user}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
</beans>
```

d) 配置C3P0连接池；

```xml
<!--数据源-->
    <context:property-placeholder location="db.properties"/><!--读取配置文件-->
    <bean name="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"><!--配置DataSource-->
        <property name="driverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>
        <property name="user" value="${jdbc.user}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
```

e) 读取db.properties；

```properties
jdbc.driverClass=com.mysql.cj.jdbc.Driver
jdbc.jdbcUrl=jdbc:mysql://localhost:3306/ssm_spring?serverTimezone=Asia/Shanghai
jdbc.user=root
jdbc.password=10709991
```

f) 配置sqlSessionFactory；

```xml
<!--mybatis-->
    <bean name="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--配置数据源-->
        <property name="dataSource" ref="dataSource"/>
        <!--告知Spring MyBatis的核心配置文件-->
        <property name="configLocation" value="classpath:sqlMapConfig.xml"/>
    </bean>
```

g) 测试

```java
ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
        SqlSessionFactoryBean sqlSessionFactoryBean = ac.getBean(SqlSessionFactoryBean.class);
System.out.println(sqlSessionFactoryBean);
```

### 3、 Dao式开发；

```xml
<!-- userDao -->
	<bean id="userDaoImpl" class="com.sikiedu.dao.UserDaoImpl">
		<!-- 将工厂注入到dao的父类 sqlSessionFactory -->
		<property name="sqlSessionFactory" ref="sqlSessionFactoryBean"/>
	</bean>
```

### 4、 Mapper动态代理开发；

```xml
<!-- mapper动态代理开发 -->
	<bean id="userMapper" class="org.mybatis.spring.mapper.MapperFactoryBean">
		<!-- 注入 sqlSessionFactory -->
		<property name="sqlSessionFactory" ref="sqlSessionFactoryBean"/>
		<!-- 配置接口 -->
		<property name="mapperInterface" value="com.sikiedu.mapper.UserMapper"/>
	</bean>
```

### 5、 Mapper动态扫描开发：不需要配置多个接口；

```xml
<!-- mapper动态扫描开发 -->
	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
		<property name="basePackage" value="com.sikiedu.mapper"/>
	</bean>
```

part11、未完待续……
--------------------------------------------------------------