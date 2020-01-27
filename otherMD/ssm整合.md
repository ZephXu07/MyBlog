[![](/assets/img/HeadFish.jpg)](/)

[ZephXu07](/) []
=============

-   [主页](/)
-   [笔记](/tags/笔记/)
-   [归档](/archives/index.html)

[所有文章](javascript:void(0)) [友链](javascript:void(0))
[关于我](javascript:void(0))

[**](https://github.com/ZephXu07 "github")
[**](https://weibo.com/5409078656/profile?rightmod=1&wvr=6&mod=personinfo&is_all=1 "weibo")
[**](https://space.bilibili.com/14445452 "bilibili")

**

![](/assets/img/HeadFish.jpg)

ZephXu07 []
========

[**](https://github.com/ZephXu07 "github")
[**](https://weibo.com/5409078656/profile?rightmod=1&wvr=6&mod=personinfo&is_all=1 "weibo")
[**](https://space.bilibili.com/14445452 "bilibili")

-   [主页](/)
-   [笔记](/tags/笔记/)
-   [归档](/archives/index.html)

SSM框架整合 []
===========


 [阅读数: 次   ](javascript:void(0);)
[**2019-10-15](/2019/10/15/SSM框架整合/)

[](#part1、搭建整合环境 "part1、搭建整合环境")part1、搭建整合环境
=================================================================

![Structure](https://github.com/ZephXu07/IMG/raw/master/Structure.png)

[](#1、整合说明： "1、整合说明：")1、整合说明： [1、整合说明：]
-----------------------------------------------

SSM整合可以使用多种方式，此次选择XML + 注解的方式

[](#2、整合的思路 "2、整合的思路")2、整合的思路 [2、整合的思路]
-----------------------------------------------

### [](#a-、先搭建整合的环境 "a)、先搭建整合的环境")a)、先搭建整合的环境 [a-、先搭建整合的环境]

### [](#b-、先把Spring的配置搭建完成 "b)、先把Spring的配置搭建完成")b)、先把Spring的配置搭建完成 [b-、先把Spring的配置搭建完成]

### [](#c-、再使用Spring整合SpringMVC框架 "c)、再使用Spring整合SpringMVC框架")c)、再使用Spring整合SpringMVC框架 [c-、再使用Spring整合SpringMVC框架]

### [](#d-、最后使用Spring整合MyBatis框架 "d)、最后使用Spring整合MyBatis框架")d)、最后使用Spring整合MyBatis框架 [d-、最后使用Spring整合MyBatis框架]

[](#3、创建数据库和表结构 "3、创建数据库和表结构")3、创建数据库和表结构 [3、创建数据库和表结构]
-----------------------------------------------------------------------

-   语句

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567</code></pre></td>
<td align="left"><pre><code>create database ssm; use ssm; create table account(     id int primary key auto_increment,     name varchar(20),     money double);</code></pre></td>
</tr>
</tbody>
</table>

[](#4、创建maven的工程（使用到工程的聚合和拆分的概念） "4、创建maven的工程（使用到工程的聚合和拆分的概念）")4、创建maven的工程（使用到工程的聚合和拆分的概念） [4、创建maven的工程（使用到工程的聚合和拆分的概念）]
--------------------------------------------------------------------------------------------------------------------------------------------------------------

-   a)、创建ssm\_parent父工程（打包方式选择pom，必须的）

-   b)、创建ssm\_web子模块（打包方式是war包）

-   c)、创建ssm\_service子模块（打包方式是jar包）

-   d)、创建ssm\_dao子模块（打包方式是jar包）

-   e)、创建ssm\_domain子模块（打包方式是jar包）

-   f)、web依赖于service，service依赖于dao，dao依赖于domain

-   g)、在ssm\_parent的pom.xml文件中引入坐标依赖

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109</code></pre></td>
<td align="left"><pre><code>&lt;properties&gt;    &lt;spring.version&gt;5.2.0.RELEASE&lt;/spring.version&gt;    &lt;slf4j.version&gt;2.0.0-alpha1&lt;/slf4j.version&gt;    &lt;log4j.version&gt;1.2.17&lt;/log4j.version&gt;    &lt;mybatis.version&gt;3.5.2&lt;/mybatis.version&gt;    &lt;mysql.version&gt;8.0.17&lt;/mysql.version&gt;&lt;/properties&gt;&lt;!--版本锁定--&gt; &lt;dependencies&gt;    &lt;!-- spring --&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.aspectj&lt;/groupId&gt;      &lt;artifactId&gt;aspectjweaver&lt;/artifactId&gt;      &lt;version&gt;1.9.4&lt;/version&gt;  &lt;/dependency&gt;  &lt;dependency&gt;     &lt;groupId&gt;org.springframework&lt;/groupId&gt;     &lt;artifactId&gt;spring-aop&lt;/artifactId&gt;     &lt;version&gt;${spring.version}&lt;/version&gt;   &lt;/dependency&gt;   &lt;dependency&gt;     &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-context&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-web&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-webmvc&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-test&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-tx&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-jdbc&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;      &lt;!-- https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api --&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.junit.jupiter&lt;/groupId&gt;      &lt;artifactId&gt;junit-jupiter-api&lt;/artifactId&gt;      &lt;version&gt;5.5.2&lt;/version&gt;      &lt;scope&gt;test&lt;/scope&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;mysql&lt;/groupId&gt;      &lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;      &lt;version&gt;${mysql.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api --&gt;    &lt;dependency&gt;      &lt;groupId&gt;javax.servlet&lt;/groupId&gt;      &lt;artifactId&gt;javax.servlet-api&lt;/artifactId&gt;      &lt;version&gt;4.0.1&lt;/version&gt;      &lt;scope&gt;provided&lt;/scope&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api --&gt;    &lt;dependency&gt;      &lt;groupId&gt;javax.servlet.jsp&lt;/groupId&gt;      &lt;artifactId&gt;javax.servlet.jsp-api&lt;/artifactId&gt;      &lt;version&gt;2.3.3&lt;/version&gt;      &lt;scope&gt;provided&lt;/scope&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl-api --&gt;    &lt;dependency&gt;      &lt;groupId&gt;javax.servlet.jsp.jstl&lt;/groupId&gt;      &lt;artifactId&gt;jstl-api&lt;/artifactId&gt;      &lt;version&gt;1.2&lt;/version&gt;    &lt;/dependency&gt;    &lt;!-- log start --&gt;    &lt;dependency&gt;      &lt;groupId&gt;log4j&lt;/groupId&gt;      &lt;artifactId&gt;log4j&lt;/artifactId&gt;      &lt;version&gt;${log4j.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.slf4j&lt;/groupId&gt;      &lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;      &lt;version&gt;${slf4j.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.slf4j&lt;/groupId&gt;      &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;      &lt;version&gt;${slf4j.version}&lt;/version&gt;    &lt;/dependency&gt; &lt;!-- log end --&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.mybatis&lt;/groupId&gt;      &lt;artifactId&gt;mybatis&lt;/artifactId&gt;      &lt;version&gt;${mybatis.version}&lt;/version&gt;  &lt;/dependency&gt;&lt;/dependencies&gt;</code></pre></td>
</tr>
</tbody>
</table>

-   h)、部署ssm\_web的项目，只要把ssm\_web项目加入到tomcat服务器中即可

[](#5、编写domain实体类 "5、编写domain实体类")5、编写domain实体类 [5、编写domain实体类]
-----------------------------------------------------------------

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617181920212223242526272829303132333435363738394041</code></pre></td>
<td align="left"><pre><code>/** * @author: zephxu * @email: zephaniaxu0701@gmail.com * PACKAGE: com.zephxu.domain * PROJECT: ssm * Date: 2019-10-15 20:06 * @module: 类所属模块 * @describe: 账户 * @version: v1.0 */package com.zephxu.domain;public class Account {    private Integer id;    private Double money;    private String name;    public Integer getId() {        return id;    }    public void setId(Integer id) {        this.id = id;    }    public Double getMoney() {        return money;    }    public void setMoney(Double money) {        this.money = money;    }    public String getName() {        return name;    }    public void setName(String name) {        this.name = name;    }}</code></pre></td>
</tr>
</tbody>
</table>

[](#6、编写dao接口 "6、编写dao接口")6、编写dao接口 [6、编写dao接口]
--------------------------------------------------

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324252627282930</code></pre></td>
<td align="left"><pre><code>/** * @author: zephxu * @email: zephaniaxu0701@gmail.com * PACKAGE: com.zephxu.dao * PROJECT: ssm * Date: 2019-10-15 20:09 * @module: 类所属模块 * @describe: 账户dao接口 * @version: v1.0 */package com.zephxu.dao;import com.zephxu.domain.Account;import java.util.List;public interface IAccountDao {    /**     *     * @return 查询的所有账户     */    public List&lt;Account&gt; findAll();    /**     *     * @param account 所要保存的账户     */    public void saveAccount(Account account);}</code></pre></td>
</tr>
</tbody>
</table>

[](#7、编写service接口和实现类 "7、编写service接口和实现类")7、编写service接口和实现类 [7、编写service接口和实现类]
--------------------------------------------------------------------------------------

-   接口：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617181920212223242526272829</code></pre></td>
<td align="left"><pre><code>/** * @author: zephxu * @email: zephaniaxu0701@gmail.com * PACKAGE: com.zephxu.service * PROJECT: ssm * Date: 2019-10-15 21:49 * @module: 类所属模块 * @describe: * @version: v1.0 */package com.zephxu.service;import com.zephxu.domain.Account;import java.util.List;public interface IAccountService {    /**     *     * @return 查询的所有账户     */    public List&lt;Account&gt; findAll();    /**     *     * @param account 所要保存的账户     */    public void saveAccount(Account account);}</code></pre></td>
</tr>
</tbody>
</table>

-   实现类：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324252627282930</code></pre></td>
<td align="left"><pre><code>/** * @author: zephxu * @email: zephaniaxu0701@gmail.com * PACKAGE: com.zephxu.service.impl * PROJECT: ssm * Date: 2019-10-15 21:50 * @module: 类所属模块 * @describe: * @version: v1.0 */package com.zephxu.service.impl;import com.zephxu.domain.Account;import com.zephxu.service.IAccountService;import java.util.List;@Service(&quot;accountService&quot;)public class AccountServiceImpl implements IAccountService {    @Override    public List&lt;Account&gt; findAll() {        System.out.println(&quot;业务层：查询所有账户&quot;);        return null;    }    @Override    public void saveAccount(Account account) {        System.out.println(&quot;业务层：保存账户&quot;);    }}</code></pre></td>
</tr>
</tbody>
</table>

[](#part2、Spring框架代码的编写 "part2、Spring框架代码的编写")part2、Spring框架代码的编写 [part2、Spring框架代码的编写]
=========================================================================================

[](#搭建和测试Spring的开发环境 "搭建和测试Spring的开发环境")搭建和测试Spring的开发环境 [搭建和测试Spring的开发环境]
--------------------------------------------------------------------------------------

### [](#1、创建applicationContext-xml的配置文件，编写具体的配置信息 "1、创建applicationContext.xml的配置文件，编写具体的配置信息")1、创建applicationContext.xml的配置文件，编写具体的配置信息 [1、创建applicationContext-xml的配置文件，编写具体的配置信息]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617181920</code></pre></td>
<td align="left"><pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;&lt;beans xmlns=&quot;http://www.springframework.org/schema/beans&quot;       xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot;       xmlns:context=&quot;http://www.springframework.org/schema/context&quot;       xmlns:aop=&quot;http://www.springframework.org/schema/aop&quot;       xmlns:tx=&quot;http://www.springframework.org/schema/tx&quot;       xsi:schemaLocation=&quot;http://www.springframework.org/schema/beans   http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context    http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/aop    http://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd&quot;&gt;    &lt;!--开启注解扫描，希望处理service和dao，controller不需要Spring处理--&gt;    &lt;context:component-scan base-package=&quot;com.zephxu&quot;&gt;        &lt;!--此注解不被扫描--&gt;        &lt;context:exclude-filter type=&quot;annotation&quot; expression=&quot;org.springframework.stereotype.Controller&quot;/&gt;    &lt;/context:component-scan&gt;&lt;/beans&gt;</code></pre></td>
</tr>
</tbody>
</table>

### [](#2、编写测试方法，进行测试，点击查看详情 "2、编写测试方法，进行测试，点击查看详情")2、编写测试方法，进行测试，[点击查看详情](https://zephxu07.github.io/2019/09/27/Spring-Learning-Notes/#3%E3%80%81-Spring-amp-JUnit%E8%BF%9B%E8%A1%8C%E6%B5%8B%E8%AF%95%EF%BC%9A) [2、编写测试方法，进行测试，点击查看详情]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324252627282930</code></pre></td>
<td align="left"><pre><code>/** * @author: zephxu * @email: zephaniaxu0701@gmail.com * PACKAGE: com.zephxu.test * PROJECT: ssm * Date: 2019-10-15 23:04 * @module: 类所属模块 * @describe: * @version: v1.0 */package com.zephxu.test;import com.zephxu.service.IAccountService;import org.junit.Test;import org.junit.runner.RunWith;import org.springframework.test.context.ContextConfiguration;import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;import javax.annotation.Resource;@RunWith(SpringJUnit4ClassRunner.class)@ContextConfiguration(&quot;classpath:applicationContext.xml&quot;)public class TestSpring {    @Resource(name = &quot;accountService&quot;)    private IAccountService accountService;    @Test    public void run1() {        accountService.findAll();    }}</code></pre></td>
</tr>
</tbody>
</table>

### [](#3、结果： "3、结果：")3、结果： [3、结果：]

**业务层：查询所有账户**

[](#part3、Spring整合SpringMVC框架 "part3、Spring整合SpringMVC框架")part3、Spring整合SpringMVC框架 [part3、Spring整合SpringMVC框架]
==================================================================================================

### [](#1、搭建和测试SpringMVC的开发环境 "1、搭建和测试SpringMVC的开发环境")1、搭建和测试SpringMVC的开发环境 [1、搭建和测试SpringMVC的开发环境]

#### [](#a-、在web-xml中配置DispatcherServlet前端控制器 "a)、在web.xml中配置DispatcherServlet前端控制器")a)、在web.xml中配置DispatcherServlet前端控制器 [a-、在web-xml中配置DispatcherServlet前端控制器]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718</code></pre></td>
<td align="left"><pre><code>&lt;!-- SpringMVC的核心前端控制器 --&gt;  &lt;servlet&gt;    &lt;servlet-name&gt;dispatcherServlet&lt;/servlet-name&gt;    &lt;servlet-class&gt;org.springframework.web.servlet.DispatcherServlet&lt;/servlet-class&gt;    &lt;!-- 配置Servlet的初始化参数，读取springmvc的配置文件，创建spring容器 --&gt;    &lt;init-param&gt;      &lt;param-name&gt;contextConfigLocation&lt;/param-name&gt;      &lt;!--给上面的DispatcherServlet类的contextConfigLocation传值，读取配置文件--&gt;      &lt;param-value&gt;classpath:SpringMVC.xml&lt;/param-value&gt;    &lt;/init-param&gt;    &lt;!--&lt;配置servlet启动时加载对象，DispatcherServlet第一次发请求时被创建--&gt;    &lt;load-on-startup&gt;1&lt;/load-on-startup&gt;  &lt;/servlet&gt;  &lt;servlet-mapping&gt;    &lt;servlet-name&gt;dispatcherServlet&lt;/servlet-name&gt;    &lt;url-pattern&gt;/&lt;/url-pattern&gt;    &lt;!--&quot;/&quot;发送任何请求都会经过DispatcherServlet--&gt;  &lt;/servlet-mapping&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#b-、在web-xml中配置DispatcherServlet过滤器解决中文乱码 "b)、在web.xml中配置DispatcherServlet过滤器解决中文乱码")b)、在web.xml中配置DispatcherServlet过滤器解决中文乱码 [b-、在web-xml中配置DispatcherServlet过滤器解决中文乱码]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213</code></pre></td>
<td align="left"><pre><code>&lt;!-- 配置解决中文乱码的过滤器 --&gt;&lt;filter&gt;   &lt;filter-name&gt;characterEncodingFilter&lt;/filter-name&gt;   &lt;filter-class&gt;org.springframework.web.filter.CharacterEncodingFilter&lt;/filter-class&gt;   &lt;init-param&gt;     &lt;param-name&gt;encoding&lt;/param-name&gt;     &lt;param-value&gt;UTF-8&lt;/param-value&gt;   &lt;/init-param&gt;&lt;/filter&gt;&lt;filter-mapping&gt;   &lt;filter-name&gt;characterEncodingFilter&lt;/filter-name&gt;   &lt;url-pattern&gt;/*&lt;/url-pattern&gt;&lt;/filter-mapping&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#c-、创建springmvc-xml的配置文件，编写配置文件 "c)、创建springmvc.xml的配置文件，编写配置文件")c)、创建springmvc.xml的配置文件，编写配置文件 [c-、创建springmvc-xml的配置文件，编写配置文件]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819</code></pre></td>
<td align="left"><pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt; &lt;beans xmlns=&quot;http://www.springframework.org/schema/beans&quot; xmlns:mvc=&quot;http://www.springframework.org/schema/mvc&quot;xmlns:context=&quot;http://www.springframework.org/schema/context&quot; xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xsi:schemaLocation=&quot; http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd&quot;&gt; &lt;!-- 扫描controller的注解，别的不扫描 --&gt;           &lt;context:component-scan base-package=&quot;com.zephxu&quot;&gt;         &lt;context:include-filter type=&quot;annotation&quot; expression=&quot;org.springframework.stereotype.Controller&quot;/&gt;     &lt;/context:component-scan&gt;    &lt;!-- 配置视图解析器 --&gt;     &lt;bean id=&quot;internalResourceViewResolver&quot; class=&quot;org.springframework.web.servlet.view.InternalResourceViewResolver&quot;&gt;        &lt;property name=&quot;prefix&quot; value=&quot;/WEB-INF/pages/&quot;/&gt;        &lt;property name=&quot;suffix&quot; value=&quot;.jsp&quot;/&gt;    &lt;/bean&gt;    &lt;!--过滤静态资源--&gt;&lt;!--    &lt;mvc:resources location=&quot;/css/&quot; mapping=&quot;/css/**&quot; /&gt;--&gt;&lt;!--    &lt;mvc:resources location=&quot;/images/&quot; mapping=&quot;/images/**&quot; /&gt;--&gt;&lt;!--    &lt;mvc:resources location=&quot;/js/&quot; mapping=&quot;/js/**&quot; /&gt;--&gt;    &lt;!--开启SpringMVC注解的支持--&gt;    &lt;mvc:annotation-driven/&gt;&lt;/beans&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#d-、测试SpringMVC的框架搭建是否成功 "d)、测试SpringMVC的框架搭建是否成功")d)、测试SpringMVC的框架搭建是否成功 [d-、测试SpringMVC的框架搭建是否成功]

##### [](#i-编写index-jsp和list-jsp编写，超链接 "i)编写index.jsp和list.jsp编写，超链接")i)编写index.jsp和list.jsp编写，超链接 [i-编写index-jsp和list-jsp编写，超链接]

index,jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789</code></pre></td>
<td align="left"><pre><code>&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;SSM&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&lt;a href=&quot;account/findAll&quot;&gt;测试&lt;/a&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

list.jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789</code></pre></td>
<td align="left"><pre><code>&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;List&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&lt;h1&gt;查询所有账户&lt;/h1&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

##### [](#ii-、创建AccountController类，编写方法，进行测试 "ii)、创建AccountController类，编写方法，进行测试")ii)、创建AccountController类，编写方法，进行测试 [ii-、创建AccountController类，编写方法，进行测试]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789</code></pre></td>
<td align="left"><pre><code>@Controller@RequestMapping(&quot;/account&quot;)public class AccountController {    @RequestMapping(&quot;/findAll&quot;)    public String findAll() {        System.out.println(&quot;表现层：查询所有账户&quot;);        return &quot;list&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

### [](#2、Spring整合SpringMVC的框架 "2、Spring整合SpringMVC的框架")2、Spring整合SpringMVC的框架 [2、Spring整合SpringMVC的框架]

![Conformity](https://github.com/ZephXu07/IMG/raw/master/SpringConformitySpringMVC.png)

#### [](#a-、目的：在controller中能成功的调用service对象中的方法。 "a)、目的：在controller中能成功的调用service对象中的方法。")a)、目的：在controller中能成功的调用service对象中的方法。 [a-、目的：在controller中能成功的调用service对象中的方法。]

#### [](#b-、注意： "b)、注意：")b)、注意： [b-、注意：]

**在项目启动的时候，就去加载applicationContext.xml的配置文件（没有配置时不会被加载），在web.xml中配置
ContextLoaderListener监听器（该监听器只能加载WEB-INF目录下的applicationContext.xml的配置文
件）。[（前面Spring提及）](https://zephxu07.github.io/2019/09/27/Spring-Learning-Notes/#ii-%E5%9C%A8web-xml%E4%B8%AD%E9%85%8D%E7%BD%AESpring%E7%9B%91%E5%90%AC%E5%99%A8%E5%92%8C%E8%AF%BB%E5%8F%96%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%EF%BC%9B)**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789</code></pre></td>
<td align="left"><pre><code>&lt;listener&gt;    &lt;!--配置Spring的监听器，默认只加载WEB-INF目录下的applicationContext.xml配置文件--&gt;    &lt;listener-class&gt;org.springframework.web.context.ContextLoaderListener&lt;/listener-class&gt;  &lt;/listener&gt;  &lt;!--设置配置文件的路径--&gt;  &lt;context-param&gt;    &lt;param-name&gt;contextConfigLocation&lt;/param-name&gt;    &lt;param-value&gt;classpath:applicationContext.xml&lt;/param-value&gt;  &lt;/context-param&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#c-、在controller中注入service对象，调用service对象的方法进行测试 "c)、在controller中注入service对象，调用service对象的方法进行测试")c)、在controller中注入service对象，调用service对象的方法进行测试 [c-、在controller中注入service对象，调用service对象的方法进行测试]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415</code></pre></td>
<td align="left"><pre><code>@Controller@RequestMapping(&quot;/account&quot;)public class AccountController {    //注入    @Resource(name = &quot;accountService&quot;)    private IAccountService accountService;    @RequestMapping(&quot;/findAll&quot;)    public String findAll() {        System.out.println(&quot;表现层：查询所有账户&quot;);        accountService.findAll();        return &quot;list&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

#### [](#d-、结果： "d)、结果：")d)、结果： [d-、结果：]

**表现层：查询所有账户  
 业务层：查询所有账户**

[](#part4、Spring整合MyBatis框架 "part4、Spring整合MyBatis框架")part4、Spring整合MyBatis框架 [part4、Spring整合MyBatis框架]
============================================================================================

[](#1、搭建和测试MyBatis的环境 "1、搭建和测试MyBatis的环境")1、搭建和测试MyBatis的环境 [1、搭建和测试MyBatis的环境]
--------------------------------------------------------------------------------------

### [](#a-、在web项目中编写SqlMapConfig-xml的配置文件，编写核心配置文件 "a)、在web项目中编写SqlMapConfig.xml的配置文件，编写核心配置文件")a)、在web项目中编写SqlMapConfig.xml的配置文件，编写核心配置文件 [a-、在web项目中编写SqlMapConfig-xml的配置文件，编写核心配置文件]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819202122232425</code></pre></td>
<td align="left"><pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;&lt;!DOCTYPE configuration        PUBLIC &quot;-//mybatis.org//DTD Config 3.0//EN&quot;        &quot;http://mybatis.org/dtd/mybatis-3-config.dtd&quot;&gt;&lt;configuration&gt;    &lt;!-- 读取配置文件 --&gt;    &lt;properties resource=&quot;db.properties&quot;/&gt;    &lt;!--配置环境--&gt;    &lt;environments default=&quot;mysql&quot;&gt;        &lt;environment id=&quot;mysql&quot;&gt;            &lt;transactionManager type=&quot;JDBC&quot;/&gt;            &lt;dataSource type=&quot;POOLED&quot;&gt;                &lt;property name=&quot;driver&quot; value=&quot;${jdbc.driver}&quot;/&gt;                &lt;property name=&quot;url&quot; value=&quot;${jdbc.url}&quot;/&gt;                &lt;property name=&quot;username&quot; value=&quot;${jdbc.username}&quot;/&gt;                &lt;property name=&quot;password&quot; value=&quot;${jdbc.password}&quot;/&gt;            &lt;/dataSource&gt;        &lt;/environment&gt;    &lt;/environments&gt;    &lt;!--引入配置文件，使用注解--&gt;    &lt;mappers&gt;        &lt;package name=&quot;com.zephxu.dao&quot;/&gt;    &lt;/mappers&gt;&lt;/configuration&gt;</code></pre></td>
</tr>
</tbody>
</table>

### [](#b-、在IAccountDao接口的方法上添加注解，编写SQL语句 "b)、在IAccountDao接口的方法上添加注解，编写SQL语句")b)、在IAccountDao接口的方法上添加注解，编写SQL语句 [b-、在IAccountDao接口的方法上添加注解，编写SQL语句]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415</code></pre></td>
<td align="left"><pre><code>public interface IAccountDao {    /**     *     * @return 查询的所有账户     */    @Select(&quot;select * from account&quot;)    public List&lt;Account&gt; findAll();    /**     *     * @param account 所要保存的账户     */    @Insert(&quot;insert into account (name, money) values (#{name}, #{money}&quot;)    public void saveAccount(Account account);}</code></pre></td>
</tr>
</tbody>
</table>

### [](#c-、编写测试的方法 "c)、编写测试的方法")c)、编写测试的方法 [c-、编写测试的方法]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819202122232425262728</code></pre></td>
<td align="left"><pre><code>public class TestMyBatis {    @Test    public void run() throws IOException {        //加载配置文件        InputStream in = Resources.getResourceAsStream(&quot;sqlMapConfig.xml&quot;);        //创建SqlSessionFactory对象        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(in);        //创建SqlSession        SqlSession session = factory.openSession();        //获取代理对象        IAccountDao accountDao = session.getMapper(IAccountDao.class);        //插入数据        Account account = new Account();        account.setName(&quot;xhy&quot;);        account.setMoney(100000D);        accountDao.saveAccount(account);        // 提交事务        session.commit();        //查询所有数据        List&lt;Account&gt; accountList = accountDao.findAll();        for (Account a:accountList) {            System.out.println(a);        }        //关闭资源        session.close();        in.close();    }}</code></pre></td>
</tr>
</tbody>
</table>

[](#2、Spring整合MyBatis框架 "2、Spring整合MyBatis框架")2、Spring整合MyBatis框架 [2、Spring整合MyBatis框架]
--------------------------------------------------------------------------------

### [](#a-、整合思路： "a)、整合思路：")a)、整合思路： [a-、整合思路：]

把 mybatis 配置文件（SqlMapConfig.xml）中内容配置到 spring 配置文件中
同时，把 mybatis 配置文件的内容清掉。

### [](#b-、目的： "b)、目的：")b)、目的： [b-、目的：]

把SqlMapConfig.xml配置文件中的内容配置到applicationContext.xml配置文件中。

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819</code></pre></td>
<td align="left"><pre><code>&lt;!--Spring整合MyBatis框架--&gt;    &lt;!--配置连接池--&gt;    &lt;!--读取配置文件--&gt;    &lt;context:property-placeholder location=&quot;classpath:db.properties&quot;/&gt;    &lt;bean id=&quot;dataSource&quot; class=&quot;com.mchange.v2.c3p0.ComboPooledDataSource&quot;&gt;        &lt;property name=&quot;driverClass&quot; value=&quot;${jdbc.driver}&quot;/&gt;        &lt;property name=&quot;jdbcUrl&quot; value=&quot;${jdbc.url}&quot;/&gt;        &lt;property name=&quot;user&quot; value=&quot;${jdbc.username}&quot;/&gt;        &lt;property name=&quot;password&quot; value=&quot;${jdbc.password}&quot;/&gt;    &lt;/bean&gt;    &lt;!--配置SqlSessionFactory工厂--&gt;    &lt;bean id=&quot;sqlSessionFactory&quot; class=&quot;org.mybatis.spring.SqlSessionFactoryBean&quot;&gt;        &lt;!--配置数据源--&gt;        &lt;property name=&quot;dataSource&quot; ref=&quot;dataSource&quot;/&gt;    &lt;/bean&gt;    &lt;!--配置AccountDao--&gt;    &lt;bean id=&quot;mapperScanner&quot; class=&quot;org.mybatis.spring.mapper.MapperScannerConfigurer&quot;&gt;        &lt;property name=&quot;basePackage&quot; value=&quot;com.zephxu&quot;/&gt;    &lt;/bean&gt;</code></pre></td>
</tr>
</tbody>
</table>

### [](#c-、在AccountDao接口中添加-Repository注解 "c)、在AccountDao接口中添加@Repository注解")c)、在AccountDao接口中添加@Repository注解 [c-、在AccountDao接口中添加-Repository注解]

### [](#d-、在service中注入dao对象，进行测试 "d)、在service中注入dao对象，进行测试")d)、在service中注入dao对象，进行测试 [d-、在service中注入dao对象，进行测试]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12</code></pre></td>
<td align="left"><pre><code>@Autowiredprivate IAccountDao accountDao;</code></pre></td>
</tr>
</tbody>
</table>

### [](#e-、代码： "e)、代码：")e)、代码： [e-、代码：]

list.jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213</code></pre></td>
<td align="left"><pre><code>&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; isELIgnored=&quot;false&quot; %&gt;&lt;%@ taglib prefix=&quot;c&quot; uri=&quot;http://java.sun.com/jsp/jstl/core&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;List&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&lt;h1&gt;查询所有账户&lt;/h1&gt;&lt;c:forEach items=&quot;${list}&quot; var=&quot;account&quot;&gt;    ${account.toString()}&lt;/c:forEach&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

### [](#f-、BUG或注意事项： "f)、BUG或注意事项：")f)、BUG或注意事项： [f-、BUG或注意事项：]

#### [](#i-、web-xml配置顺序： "i)、web.xml配置顺序：")i)、web.xml配置顺序： [i-、web-xml配置顺序：]

icon?,display-name?,description?,distributable?,context-param*,filter*,filter-mapping*,listener*,servlet*,servlet-mapping*,session-config?,mime-mapping*,welcome-file-list?,error-page*,taglib*,resource-env-ref*,resource-ref*,security-constraint*,login-config?,security-role*,env-entry*,ejb-ref,ejb-local-ref

#### [](#ii-、BUG1： "ii)、BUG1：")ii)、BUG1： [ii-、BUG1：]

**Caused by: java.io.FileNotFoundException: Could not open
ServletContext resource [/db.properties]**或者**Could not load
properties; nested exception is java.io.FileNotFoundException: Could not
open ServletContext resource [/db.properties]**

-   [解决](https://blog.csdn.net/qq_37937144/article/details/89549141)

#### [](#iii-、BUG2： "iii)、BUG2：")iii)、BUG2： [iii-、BUG2：]

**java.lang.ClassNotFoundException:org.apache.taglibs.standard.tlv.JstlCoreTLV**

**原因：jstl
1.2jar包没导入或者[导入其他两个jar包](https://blog.csdn.net/weixin_42324489/article/details/81019996)**

### [](#g-、配置Spring的声明式事务管理（更加具体的aop事务） "g)、配置Spring的声明式事务管理（更加具体的aop事务）")g)、配置Spring的声明式事务管理[（更加具体的aop事务）](https://zephxu07.github.io/2019/09/27/Spring-Learning-Notes/#part7-Spring%E4%B8%AD%E7%9A%84aop%E4%BA%8B%E5%8A%A1) [g-、配置Spring的声明式事务管理（更加具体的aop事务）]

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617</code></pre></td>
<td align="left"><pre><code>&lt;!--配置Spring框架声明式事务管理--&gt;    &lt;!--配置事务管理器--&gt;    &lt;bean id=&quot;transactionManager&quot; class=&quot;org.springframework.jdbc.datasource.DataSourceTransactionManager&quot;&gt;        &lt;property name=&quot;dataSource&quot; ref=&quot;dataSource&quot;/&gt;    &lt;/bean&gt;    &lt;!--配置事务通知--&gt;    &lt;tx:advice id=&quot;txAdvice&quot; transaction-manager=&quot;transactionManager&quot;&gt;        &lt;tx:attributes&gt;            &lt;tx:method name=&quot;find*&quot;/&gt;            &lt;tx:method name=&quot;*&quot;/&gt;        &lt;/tx:attributes&gt;    &lt;/tx:advice&gt;    &lt;!--配置aop增强--&gt;    &lt;aop:config&gt;        &lt;aop:advisor advice-ref=&quot;txAdvice&quot;                     pointcut=&quot;execution(* com.zephxu.service.impl.*ServiceImpl.*(..))&quot;/&gt;    &lt;/aop:config&gt;</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/save&quot;)    public void save(Account account, HttpServletRequest request, HttpServletResponse response) throws IOException {        System.out.println(&quot;表现层：保存账户&quot;);        accountService.saveAccount(account);        response.sendRedirect(request.getContextPath() + &quot;/account/findAll&quot;);    }</code></pre></td>
</tr>
</tbody>
</table>

[](#part5、未完待续…… "part5、未完待续……")part5、未完待续…… [part5、未完待续……]
===========================================================

[](javascript:;)

赏

**谢谢你请我吃糖果**

![](/assets/img/alipay.jpg) 支付宝

![](/assets/img/wechatpay.png) 微信

**

-   [笔记](javascript:void(0))
-   [Spring](javascript:void(0))
-   [MyBatis](javascript:void(0))
-   [SpringMVC](javascript:void(0))
-   [框架](javascript:void(0))
-   [java](javascript:void(0))

[**](javascript:;)

[**](javascript:;) [**](javascript:;) [**](javascript:;)
[**](javascript:;) [**](javascript:;) [**](javascript:;)
[**](javascript:;) [**](javascript:;)

[**](javascript:;)

扫一扫，分享到微信

![微信分享二维码](//pan.baidu.com/share/qrcode?url=http://yoursite.com/2019/10/15/SSM框架整合/)

[**](/2019/10/30/Practice-Project/)

Practice Project

[](/2019/10/08/百感乱记/)

百感乱记

**

[**](javascript:void(0))

**

**

1.  [1. part1、搭建整合环境](#part1、搭建整合环境)
    1.  [1.1. 1、整合说明：](#1、整合说明：)
    2.  [1.2. 2、整合的思路](#2、整合的思路)
        1.  [1.2.1. a)、先搭建整合的环境](#a-、先搭建整合的环境)
        2.  [1.2.2.
            b)、先把Spring的配置搭建完成](#b-、先把Spring的配置搭建完成)
        3.  [1.2.3.
            c)、再使用Spring整合SpringMVC框架](#c-、再使用Spring整合SpringMVC框架)
        4.  [1.2.4.
            d)、最后使用Spring整合MyBatis框架](#d-、最后使用Spring整合MyBatis框架)

    3.  [1.3. 3、创建数据库和表结构](#3、创建数据库和表结构)
    4.  [1.4.
        4、创建maven的工程（使用到工程的聚合和拆分的概念）](#4、创建maven的工程（使用到工程的聚合和拆分的概念）)
    5.  [1.5. 5、编写domain实体类](#5、编写domain实体类)
    6.  [1.6. 6、编写dao接口](#6、编写dao接口)
    7.  [1.7. 7、编写service接口和实现类](#7、编写service接口和实现类)

2.  [2. part2、Spring框架代码的编写](#part2、Spring框架代码的编写)
    1.  [2.1. 搭建和测试Spring的开发环境](#搭建和测试Spring的开发环境)
        1.  [2.1.1.
            1、创建applicationContext.xml的配置文件，编写具体的配置信息](#1、创建applicationContext-xml的配置文件，编写具体的配置信息)
        2.  [2.1.2.
            2、编写测试方法，进行测试，点击查看详情](#2、编写测试方法，进行测试，点击查看详情)
        3.  [2.1.3. 3、结果：](#3、结果：)

3.  [3. part3、Spring整合SpringMVC框架](#part3、Spring整合SpringMVC框架)
    1.  [3.0.1.
        1、搭建和测试SpringMVC的开发环境](#1、搭建和测试SpringMVC的开发环境)
        1.  [3.0.1.1.
            a)、在web.xml中配置DispatcherServlet前端控制器](#a-、在web-xml中配置DispatcherServlet前端控制器)
        2.  [3.0.1.2.
            b)、在web.xml中配置DispatcherServlet过滤器解决中文乱码](#b-、在web-xml中配置DispatcherServlet过滤器解决中文乱码)
        3.  [3.0.1.3.
            c)、创建springmvc.xml的配置文件，编写配置文件](#c-、创建springmvc-xml的配置文件，编写配置文件)
        4.  [3.0.1.4.
            d)、测试SpringMVC的框架搭建是否成功](#d-、测试SpringMVC的框架搭建是否成功)
            1.  [3.0.1.4.1.
                i)编写index.jsp和list.jsp编写，超链接](#i-编写index-jsp和list-jsp编写，超链接)
            2.  [3.0.1.4.2.
                ii)、创建AccountController类，编写方法，进行测试](#ii-、创建AccountController类，编写方法，进行测试)

    2.  [3.0.2.
        2、Spring整合SpringMVC的框架](#2、Spring整合SpringMVC的框架)
        1.  [3.0.2.1.
            a)、目的：在controller中能成功的调用service对象中的方法。](#a-、目的：在controller中能成功的调用service对象中的方法。)
        2.  [3.0.2.2. b)、注意：](#b-、注意：)
        3.  [3.0.2.3.
            c)、在controller中注入service对象，调用service对象的方法进行测试](#c-、在controller中注入service对象，调用service对象的方法进行测试)
        4.  [3.0.2.4. d)、结果：](#d-、结果：)

[4. part4、Spring整合MyBatis框架](#part4、Spring整合MyBatis框架)

1.  [4.1. 1、搭建和测试MyBatis的环境](#1、搭建和测试MyBatis的环境)
    1.  [4.1.1.
        a)、在web项目中编写SqlMapConfig.xml的配置文件，编写核心配置文件](#a-、在web项目中编写SqlMapConfig-xml的配置文件，编写核心配置文件)
    2.  [4.1.2.
        b)、在IAccountDao接口的方法上添加注解，编写SQL语句](#b-、在IAccountDao接口的方法上添加注解，编写SQL语句)
    3.  [4.1.3. c)、编写测试的方法](#c-、编写测试的方法)

2.  [4.2. 2、Spring整合MyBatis框架](#2、Spring整合MyBatis框架)
    1.  [4.2.1. a)、整合思路：](#a-、整合思路：)
    2.  [4.2.2. b)、目的：](#b-、目的：)
    3.  [4.2.3.
        c)、在AccountDao接口中添加@Repository注解](#c-、在AccountDao接口中添加-Repository注解)
    4.  [4.2.4.
        d)、在service中注入dao对象，进行测试](#d-、在service中注入dao对象，进行测试)
    5.  [4.2.5. e)、代码：](#e-、代码：)
    6.  [4.2.6. f)、BUG或注意事项：](#f-、BUG或注意事项：)
        1.  [4.2.6.1. i)、web.xml配置顺序：](#i-、web-xml配置顺序：)
        2.  [4.2.6.2. ii)、BUG1：](#ii-、BUG1：)
        3.  [4.2.6.3. iii)、BUG2：](#iii-、BUG2：)

    7.  [4.2.7.
        g)、配置Spring的声明式事务管理（更加具体的aop事务）](#g-、配置Spring的声明式事务管理（更加具体的aop事务）)

[5. part5、未完待续……](#part5、未完待续……)

© 2019 ZephXu07

[Hexo](http://hexo.io/) Theme
[Yilia](https://github.com/litten/hexo-theme-yilia) by Litten

本站总访问量次

-   [所有文章](javascript:void(0))
-   [友链](javascript:void(0))
-   [关于我](javascript:void(0))

** **

tag:

-   [Linux](javascript:void(0))
-   [基础](javascript:void(0))
-   [笔记](javascript:void(0))
-   [个人](javascript:void(0))
-   [Spring](javascript:void(0))
-   [MyBatis](javascript:void(0))
-   [SpringMVC](javascript:void(0))
-   [框架](javascript:void(0))
-   [零基础](javascript:void(0))
-   [说明](javascript:void(0))
-   [记录](javascript:void(0))
-   [Maven](javascript:void(0))
-   [工具](javascript:void(0))
-   [Java](javascript:void(0))
-   [java](javascript:void(0))

-   **

    **

    **

-   [**hexo框架](https://github.com/hexojs/hexo)
-   [**学习hexo教程](https://www.bilibili.com/video/av44544186)
-   [**yilia主题作者](https://github.com/litten/hexo-theme-yilia)
-   [**配置yilia主题博客](https://cloudy-liu.github.io/2018/04/07/Hexo_yilia_%E4%B8%BB%E9%A2%98%E4%B8%80%E6%8F%BD%E5%AD%90%E4%BC%98%E5%8C%96%E6%96%B9%E6%A1%88/#%E6%96%87%E7%AB%A0%E5%A6%82%E4%BD%95%E6%98%BE%E7%A4%BA%E6%91%98%E8%A6%81)

纯小白\<br\>\<br\>\<br\>知足常乐
