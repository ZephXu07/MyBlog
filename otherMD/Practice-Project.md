[![](/assets/img/HeadFish.jpg)](/)

[ZephXu07](/) {.header-author}
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

ZephXu07 {.header-author .js-header-author}
========

[**](https://github.com/ZephXu07 "github")
[**](https://weibo.com/5409078656/profile?rightmod=1&wvr=6&mod=personinfo&is_all=1 "weibo")
[**](https://space.bilibili.com/14445452 "bilibili")

-   [主页](/)
-   [笔记](/tags/笔记/)
-   [归档](/archives/index.html)

Practice Project {.article-title itemprop="name"}
================

\
 [阅读数: 次   ](javascript:void(0);)
[**2019-10-30](/2019/10/30/Practice-Project/)

[](#使用SSM框架开发众筹网站 "使用SSM框架开发众筹网站")使用SSM框架开发众筹网站 {#使用SSM框架开发众筹网站}
=============================================================================

[项目文件](https://github.com/ZephXu07/Atcrowdfundingparent)

[](#一、项目第一天计划 "一、项目第一天计划")一、项目第一天计划 {#一、项目第一天计划}
--------------------------------------------------------------

### [](#1、-课件目录结构介绍 "1、  课件目录结构介绍")1、 课件目录结构介绍 {#1、-课件目录结构介绍}

### [](#2、互联网金融项目背景，概念介绍 "2、互联网金融项目背景，概念介绍")2、互联网金融项目背景，概念介绍 {#2、互联网金融项目背景，概念介绍}

[资料](https://github.com/ZephXu07/IMG/blob/master/OtherInformation/01-互联网金融.pptx)

### [](#3、项目管理与环境搭建 "3、项目管理与环境搭建")3、项目管理与环境搭建 {#3、项目管理与环境搭建}

#### [](#1-、尚筹网项目构成 "(1)、尚筹网项目构成")(1)、尚筹网项目构成 {#1-、尚筹网项目构成}

##### [](#a、项目范围 "a、项目范围")a、项目范围 {#a、项目范围}

​ 众筹系统的实现

##### [](#b、人员组织结构 "b、人员组织结构")b、人员组织结构 {#b、人员组织结构}

项目经理（1） + 系统架构师（1） + 系统分析师（2） +
项目组（组长(TL)，软件工程师（SE）, 组员(PG)）（5-7）\*N

##### [](#c、项目周期（时间进度） "c、项目周期（时间进度）")c、项目周期（时间进度） {#c、项目周期（时间进度）}

​ 需求分析（20%） + 设计（30%） + 开发（20%） + 测试（30%）

#### [](#2-、尚筹网项目需求分析 "(2)、尚筹网项目需求分析")(2)、尚筹网项目需求分析 {#2-、尚筹网项目需求分析}

a、需求采集

b、需求编制

c、需求审核

​ Web项目可根据需求创建原型页面或草图设计用于确认需求。（MockupCreator）

#### [](#3-、尚筹网项目设计 "(3)、尚筹网项目设计")(3)、尚筹网项目设计 {#3-、尚筹网项目设计}

(a)、页面设计 （Frontpage, Dreamweaver， 文本编辑器）

(b)、物理数据模型（PDM） – 数据库设计 （PowerDesigner）

​ 抽取概念模型 –\> 转换对象模型 –\> 转换数据模型

(c)、业务流程设计 （UML ： 类图，时序图，用例图，页面迁移图）
(Rational\_Rose[安装教程](https://blog.csdn.net/weixin_42983731/article/details/85014298))[（UML.pptx）](https://github.com/ZephXu07/IMG/blob/master/OtherInformation/03-UML.pptx)

#### [](#4-、尚筹网-项目开发 "(4)、尚筹网 项目开发")(4)、尚筹网 项目开发 {#4-、尚筹网-项目开发}

##### [](#a-、项目环境搭建-（非常重要） "(a)、项目环境搭建 （非常重要）")(a)、项目环境搭建 （非常重要） {#a-、项目环境搭建-（非常重要）}

###### [](#i-、创建Web项目（生成基本的web应用文件结构）（普通） "(i)、创建Web项目（生成基本的web应用文件结构）（普通）")(i)、创建Web项目（生成基本的web应用文件结构）（普通） {#i-、创建Web项目（生成基本的web应用文件结构）（普通）}

WebContent(ROOT)

​ +–META-INF

​ +–WEB-INF

​ | +–classes

​ | +–lib

​ | |–web.xml

​ |–index.jsp

###### [](#ii-、修改开发工具的相关配置 "(ii)、修改开发工具的相关配置")(ii)、修改开发工具的相关配置 {#ii-、修改开发工具的相关配置}

字符编码 UTF-8

JDK版本 - 1.8

###### [](#iii-、增加基础框架的类库及相应配置文件 "(iii)、增加基础框架的类库及相应配置文件")(iii)、增加基础框架的类库及相应配置文件 {#iii-、增加基础框架的类库及相应配置文件}

SpringMVC

Spring

Mybatis

DB

WEB

###### [](#iv-、增加项目基础JAVA代码（包，接口，类） "(iv)、增加项目基础JAVA代码（包，接口，类）")(iv)、增加项目基础JAVA代码（包，接口，类） {#iv-、增加项目基础JAVA代码（包，接口，类）}

**包名起名的原则： 域名的反写(com.zephxu) + 项目名称(atcrowdfunding) +
模块名称(member) + 程序类型名称(bean)**

Bean

Controller/Handler

Service/ServiceImpl

Dao/Mapper

Util

Filter

Listener

##### [](#b-、项目代码开发 "(b)、项目代码开发")(b)、项目代码开发 {#b-、项目代码开发}

-   编码规范

-   模块开发

### [](#4、Maven项目模块划分 "4、Maven项目模块划分")4、Maven项目模块划分 {#4、Maven项目模块划分}

#### [](#1-、模块划分 "(1)、模块划分")(1)、模块划分 {#1-、模块划分}

-   Atcrowdfunding-parent 父工程,聚合其他工程(pom)
-   Atcrowdfunding-main Web工程,存放所有页面,框架配置文件(war)
-   Atcrowdfunding-manager-impl
    后台管理系统,存放控制器类,业务层实现类(jar)
-   Atcrowdfunding-manager-api
    后台管理系统,存放业务层接口和DAO层接口(jar)
-   Atcrowdfunding-potal-impl 前台系统,存放控制器类,业务层实现类(jar)
-   Atcrowdfunding-potal-api 前台系统,存放业务层接口和DAO层接口(jar)
-   Atcrowdfunding-common 存放所有模块所需要的公共类(jar)
-   Atcrowdfunding-bean 存放所有模块的实体类(jar)
-   ![partition](https://github.com/ZephXu07/IMG/raw/master/ProjectPartition.png)

#### [](#2-、模块关系 "(2)、模块关系")(2)、模块关系 {#2-、模块关系}

![](https://github.com/ZephXu07/IMG/raw/master/MavenProject.png)

#### [](#3-、注意事项 "(3)、注意事项")(3)、注意事项 {#3-、注意事项}

-   不同模块打包类型不同

+--------------------------------------+--------------------------------------+
|     123456789                        |     <parent> <artifactId>Atcrowdfund |
|                                      | ing-parent</artifactId>    <groupId> |
|                                      | com.zephxu.maven</groupId>    <versi |
|                                      | on>1.0-SNAPSHOT</version>    <relati |
|                                      | vePath>../pom.xml</relativePath></pa |
|                                      | rent><packaging>pom</packaging><pack |
|                                      | aging>jar</packaging><packaging>war< |
|                                      | /packaging>                          |
+--------------------------------------+--------------------------------------+

-   导入坐标，父工程，子工程，子工程不需要版本号

-   main模块配置

    ![mainConfiguration](https://github.com/ZephXu07/IMG/raw/master/MainConfiguration.png)

### [](#5、项目环境搭建细节 "5、项目环境搭建细节")5、项目环境搭建细节 {#5、项目环境搭建细节}

#### [](#1-、监听器： "(1)、监听器：")(1)、监听器： {#1-、监听器：}

##### [](#a、 "a、")a、 {#a、}

创建Spring容器的IOC容器，将IOC容器对象放到Application域中

`ApplicationContext ioc = WebApplicationContextUtils.getWebApplicationContext(application);`

##### [](#b、ServletContextListenner监听器接口： "b、ServletContextListenner监听器接口：")b、ServletContextListenner监听器接口： {#b、ServletContextListenner监听器接口：}

-   监听ServletContext对象创建和销毁：如果监听到ServletContext创建（服务器启动），就会创建IOC容器；如果监听到ServletContext销毁（服务器停止或者卸载项目），就会销毁IOC容器
-   -   在服务器启动时建立数据库表结构,初始化数据库.
    -   在服务器启动时,将数据库常量数据加载到内存,提供访问效率.
    -   在服务器启动时,获取项目上下文路径,存放到application域,给页面使用.
    -   存放计数器,计算在线用户数.

##### [](#c、ServletContextAttributeListener： "c、ServletContextAttributeListener：")c、ServletContextAttributeListener： {#c、ServletContextAttributeListener：}

监听ServletContext对象的属性的变化:添加,覆盖,删除

##### [](#d、HttpSessionListener "d、HttpSessionListener")d、HttpSessionListener {#d、HttpSessionListener}

监听HttpSession对象的创建和销毁

##### [](#e、HttpSessionAttributeListener "e、HttpSessionAttributeListener")e、HttpSessionAttributeListener {#e、HttpSessionAttributeListener}

监听HttpSession对象的属性变化:添加,覆盖,删除

##### [](#f、ServletRequestListener "f、ServletRequestListener")f、ServletRequestListener {#f、ServletRequestListener}

监听HttpServletRequest对象的创建和销毁

##### [](#g、ServletRequestAttributeListener "g、ServletRequestAttributeListener")g、ServletRequestAttributeListener {#g、ServletRequestAttributeListener}

监听HttpServletRequest对象的属性变化:添加,覆盖,删除

#### [](#2-、字符编码过滤器 "(2)、字符编码过滤器")(2)、字符编码过滤器 {#2-、字符编码过滤器}

##### [](#a、Web开发-javax-servlet-Filter "a、Web开发:javax.servlet.Filter")a、Web开发:javax.servlet.Filter {#a、Web开发-javax-servlet-Filter}

i、所有过滤器都应该实现Filter接口.

ii、过滤器的作用:

​ 对目标访问前或访问后进行过滤.

iii、应用场景:

-   对密码进行加密

-   对请求参数进行字符编码设置

-   对请求进行权限控制

-   对请求参数值进行非法字符过滤

##### [](#b、过滤器过滤规则 "b、过滤器过滤规则:")b、过滤器过滤规则: {#b、过滤器过滤规则}

i、过滤器默认对请求进行过滤,对服务器内部资源转发不进行过滤.

ii、需求:希望服务器**内部资源转发**也进行过滤.在中增加转发过滤设置（需要导入约束）`<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"     xmlns="http://java.sun.com/xml/ns/javaee"     xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"     id="WebApp_ID" version="2.5">`

+--------------------------------------+--------------------------------------+
|     12                               |     <dispatcher>REQUEST</dispatcher> |
|                                      | <dispatcher>FORWARD</dispatcher>     |
+--------------------------------------+--------------------------------------+

iii、过滤器过滤执行顺序:

按照匹配规则进行执行过滤（如果多个过滤器的匹配规则都匹配到这个路径,按照匹配顺序来执行过滤.
）

iv、过滤执行顺序原理:

-   通过Tomcat将过滤器对象创建后,存放到集合,然后根据匹配规则,迭代过滤器实施过滤.
-   每一个过滤器的执行有责任调用下一个过滤器的执行.所以在doFilter()方法中进行放行:
    chain.doFilter(req,resp);

![过滤器执行顺序](https://github.com/ZephXu07/IMG/raw/master/ExecutionSequence.png)

v、HiddenHttpMethodFilter

+--------------------------------------+--------------------------------------+
|     123456789                        |     <!--支持RESTful风格，将post请求转换为put或de |
|                                      | lete请求，会读取隐含参数："_method"--><filter>  |
|                                      | <filter-name>HiddenHttpMethodFilter< |
|                                      | /filter-name>    <filter-class>org.s |
|                                      | pringframework.web.filter.HiddenHttp |
|                                      | MethodFilter</filter-class></filter> |
|                                      | <filter-mapping>  <filter-name>Hidde |
|                                      | nHttpMethodFilter</filter-name>    < |
|                                      | servlet-name>springmvc</servlet-name |
|                                      | ><!--在核心控制器DispatcherServlet前执行--></ |
|                                      | filter-mapping>                      |
+--------------------------------------+--------------------------------------+

##### [](#c、项目中解决乱码问题 "c、项目中解决乱码问题")c、项目中解决乱码问题 {#c、项目中解决乱码问题}

###### [](#i、POST：字符编码过滤器只能解决POST请求乱码问题-不能解决GET请求乱码 "i、POST：字符编码过滤器只能解决POST请求乱码问题.不能解决GET请求乱码")i、POST：字符编码过滤器只能解决POST请求乱码问题.不能解决GET请求乱码 {#i、POST：字符编码过滤器只能解决POST请求乱码问题-不能解决GET请求乱码}

###### [](#ii、GET-在Tomcat-conf-server-xml中设置编码 "ii、GET: 在Tomcat/conf/server.xml中设置编码.")ii、GET: 在Tomcat/conf/server.xml中设置编码. {#ii、GET-在Tomcat-conf-server-xml中设置编码}

+--------------------------------------+--------------------------------------+
|     1                                |     <Connector port="8080" protocol= |
|                                      | "HTTP/1.1" connectionTimeout="20000" |
|                                      |  redirectPort="8443" URIEncoding="UT |
|                                      | F-8" />                              |
+--------------------------------------+--------------------------------------+

###### [](#iii、项目开发注意事项 "iii、项目开发注意事项:")iii、项目开发注意事项: {#iii、项目开发注意事项}

-   JSP页面编码设置

+--------------------------------------+--------------------------------------+
|     1                                |     <%@  page language="java" conten |
|                                      | tType="text/html; charset=UTF-8" pag |
|                                      | eEncoding="UTF-8"%>                  |
+--------------------------------------+--------------------------------------+

-   -   pageEncoding=”UTF-8” 页面编码
    -   contentType=”text/html; charset=UTF-8”
        服务器端响应返回结果字符编码:response.setCharacterEncoding(“UTF-8”);

-   数据库编码：[MySQL查看并修改当前数据库编码](https://blog.csdn.net/LTY1998/article/details/88049515)
-   -   如果修改编码:
        重新启动服务器,重新创建数据库以及表.以前创建的数据还是采用以前的编码.
    -   jdbc:mysql://localhost:3306/crowdfunding1705?rewriteBatchedStatements=true&useUnicode=true&characterEncoding=utf8
        （rewriteBatchedStatements批处理相关，characterEncoding=utf8
        指下图的中间 转换编码）

![IntermediateConversionCoding](https://github.com/ZephXu07/IMG/raw/master/IntermediateConversionCoding.png)

-   命令行查询数据显示乱码

-   -   数据库采用utf8编码,而DOS窗口默认GBK,需要通过set names
        GBK将数据库数据转换为GBK编码之后再显示到DOS窗口就解决乱码问题了.
-   -   这个设置只是临时的,只针对于当前窗口有效.

![dos窗口乱码](https://github.com/ZephXu07/IMG/raw/master/MessyCode.png)

-   Java中字符串编码转换:

    -   public byte[] getBytes(String charsetName)
        字符串对象调用这个方法将字符串转换为二进制数据(将原来编码转换为指定的中间编码)

    -   public String(byte bytes[], String charsetName)
        将二进制数组数据再转换为字符串(将数据的中间编码再转换为需要的编码).

#### [](#3-、核心控制器 "(3)、核心控制器")(3)、核心控制器 {#3-、核心控制器}

##### [](#a、注意事项 "a、注意事项")a、注意事项 {#a、注意事项}

-   错误配置：

+--------------------------------------+--------------------------------------+
|     12345                            |     <servlet-mapping>    <servlet-na |
|                                      | me>springmvc</servlet-name>    <url- |
|                                      | pattern>*.htm</url-pattern>    <url- |
|                                      | pattern>*.do</url-pattern></servlet- |
|                                      | mapping>                             |
+--------------------------------------+--------------------------------------+

-   正确配置

+--------------------------------------+--------------------------------------+
|     12345678                         |     <servlet-mapping>    <servlet-na |
|                                      | me>springmvc</servlet-name>    <url- |
|                                      | pattern>*.htm</url-pattern></servlet |
|                                      | -mapping><servlet-mapping>    <servl |
|                                      | et-name>springmvc</servlet-name>     |
|                                      | <url-pattern>*.do</url-pattern></ser |
|                                      | vlet-mapping>                        |
+--------------------------------------+--------------------------------------+

-   或者[如前文导入约束](#dtd)

##### [](#b、servlet的url-pattern匹配规则： "b、servlet的url-pattern匹配规则：")b、servlet的url-pattern匹配规则： {#b、servlet的url-pattern匹配规则：}

下面代码匹配顺序也是真正顺序。

+--------------------------------------+--------------------------------------+
|     1234567891011121314              |     <servlet-mapping>    <servlet-na |
|                                      | me>springmvc</servlet-name>    <!--精 |
|                                      | 确匹配-->    <url-pattern>/user/save</u |
|                                      | rl-pattern>    <!--路径匹配-->    <url-p |
|                                      | attern>/user/*</url-pattern>    <url |
|                                      | -pattern>/*</url-pattern>    <!--扩展匹 |
|                                      | 配-->    <url-pattern>*.htm</url-patt |
|                                      | ern>    <url-pattern>*.do</url-patte |
|                                      | rn>    <!--默认匹配-->    <url-pattern>/ |
|                                      | </url-pattern>  </servlet-mapping>   |
+--------------------------------------+--------------------------------------+

-   [更加详细介绍](https://www.cnblogs.com/canger/p/6084846.html)

-   [springmvc核心控制器配置](https://zephxu07.github.io/2019/10/05/SpringMVC-Learning-Notes/#2、配置核心的控制器（配置DispatcherServlet）)

#### [](#4-、Spring、springmvc相关配置 "(4)、Spring、springmvc相关配置")(4)、Spring、springmvc相关配置 {#4-、Spring、springmvc相关配置}

##### [](#a、spring： "a、spring：")a、spring： {#a、spring：}

-   加载外部属性配置文件

-   配置C3P0数据源

-   配置sqlSessionFactory

-   扫描Mapper映射配置

-   配置事务管理器

##### [](#b、springmvc： "b、springmvc：")b、springmvc： {#b、springmvc：}

-   a、spring：

-   字符串字符编码转换

-   -   如下配置可能只适用低版本Spring、SpringMVC或者其他原因导致现在在5.2.0.RELEASE的Spring版本中报错

+--------------------------------------+--------------------------------------+
|     1234567891011121314              |     <!-- 字符串字符编码转换 --><bean class="o |
|                                      | rg.springframework.web.servlet.mvc.a |
|                                      | nnotation.AnnotationMethodHandlerAda |
|                                      | pter" >        <property name="messa |
|                                      | geConverters">                <list> |
|                                      |                <bean class="org.spri |
|                                      | ngframework.http.converter.json.Mapp |
|                                      | ingJacksonHttpMessageConverter">     |
|                                      |                  <property name="sup |
|                                      | portedMediaTypes">                   |
|                                      |       <list>                         |
|                                      |    <value>application/json;charset=U |
|                                      | TF-8</value>                      </ |
|                                      | list>                     </property |
|                                      | >                   </bean>          |
|                                      |      </list>         </property></be |
|                                      | an>                                  |
+--------------------------------------+--------------------------------------+

-   -   改用新的设置，如下：[来源](https://www.cnblogs.com/guanghe/p/10429357.html)

+--------------------------------------+--------------------------------------+
|     12345678910111213141516171819202 |     <!-- 处理请求返回json字符串的中文乱码问题 -->  < |
| 12223242526272829303132              | mvc:annotation-driven>      <mvc:mes |
|                                      | sage-converters register-defaults="t |
|                                      | rue">          <!-- StringHttpMessag |
|                                      | eConverter编码为UTF-8，防止乱码 -->          |
|                                      |  <bean class="org.springframework.ht |
|                                      | tp.converter.StringHttpMessageConver |
|                                      | ter">              <constructor-arg  |
|                                      | value="UTF-8" />              <prope |
|                                      | rty name="supportedMediaTypes">      |
|                                      |              <list>                  |
|                                      |      <bean class="org.springframewor |
|                                      | k.http.MediaType">                   |
|                                      |        <constructor-arg index="0" va |
|                                      | lue="text" />                        |
|                                      |   <constructor-arg index="1" value=" |
|                                      | plain" />                         <c |
|                                      | onstructor-arg index="2" value="UTF- |
|                                      | 8" />                     </bean>    |
|                                      |                   <bean class="org.s |
|                                      | pringframework.http.MediaType">      |
|                                      |                     <constructor-arg |
|                                      |  index="0" value="*" />              |
|                                      |             <constructor-arg index=" |
|                                      | 1" value="*" />                      |
|                                      |     <constructor-arg index="2" value |
|                                      | ="UTF-8" />                     </be |
|                                      | an>                 </list>          |
|                                      |     </property>         </bean>      |
|                                      |     <!-- 避免IE执行AJAX时,返回JSON出现下载文件 -- |
|                                      | >         <bean id="fastJsonHttpMess |
|                                      | ageConverter"               class="c |
|                                      | om.alibaba.fastjson.support.spring.F |
|                                      | astJsonHttpMessageConverter">        |
|                                      |       <property name="supportedMedia |
|                                      | Types">                 <list>       |
|                                      |                <value>application/js |
|                                      | on;charset=UTF-8</value>             |
|                                      |      </list>             </property> |
|                                      |          </bean>     </mvc:message-c |
|                                      | onverters></mvc:annotation-driven>   |
+--------------------------------------+--------------------------------------+

-   配置只扫描controller
-   配置视图解析器
-   配置异常解析器
-   配置解析文件上传

##### [](#c、创建包结构 "c、创建包结构")c、创建包结构 {#c、创建包结构}

### [](#6、注意问题 "6、注意问题")6、注意问题 {#6、注意问题}

#### [](#1-、零容忍 "(1)、零容忍.")(1)、零容忍. {#1-、零容忍}

-   类名首字母小写.

-   参考[阿里开发规范手册](https://github.com/ZephXu07/IMG/blob/master/OtherInformation/阿里巴巴Java开发手册（详尽版）.pdf).

#### [](#2-、mybatis框架加载核心配置文件-设置的别名查找不到 "(2)、mybatis框架加载核心配置文件,设置的别名查找不到.")(2)、mybatis框架加载核心配置文件,设置的别名查找不到. {#2-、mybatis框架加载核心配置文件-设置的别名查找不到}

`<typeAlias type="User" alias="user"/>`必须指定全类名.

#### [](#3-、Service层实现类上没有增加-Service注解-导致Controller无法注入service对象 "(3)、Service层实现类上没有增加@Service注解,导致Controller无法注入service对象.")(3)、Service层实现类上没有增加@Service注解,导致Controller无法注入service对象. {#3-、Service层实现类上没有增加-Service注解-导致Controller无法注入service对象}

#### [](#4-、-Autowired进行依赖注入方式： "(4)、@Autowired进行依赖注入方式：")(4)、@Autowired进行依赖注入方式： {#4-、-Autowired进行依赖注入方式：}

##### [](#a、-1 "a、")a、 {#a、-1}

首先根据byType进行类型查找如果查找到一个,直接注入;

##### [](#b、 "b、")b、 {#b、}

如果查找到多个:
根据byName进行注入:将多个对象中其中名称与变量名称一致的那个bean注入进来.

##### [](#c、 "c、")c、 {#c、}

如果多个对象没有名称是与变量名称一致的:可以指定`@Qualifier(value="testServiceImpl")`将其中一个注入进来.如果
`@Qualifier`所指定的名称,没有与任何一个bean的名称一致,会报错.

##### [](#d、 "d、")d、 {#d、}

如果无法注入,不希望报错: `@Autowired(required=false)`

#### [](#5-、AOP动态代理相关 "(5)、AOP动态代理相关")(5)、AOP动态代理相关 {#5-、AOP动态代理相关}

**若是`private TestServiceImpl testService;`则`testService.insert();`的事务功能失效，原因是aop动态代理jdk动态代理需要目标对象有实现接口，而在容器里找到的对象是代理对象，跟目标对象只是近似的兄弟关系，并不可以通过父类转为子类导致报错，没有则是cglib动态代理，如果TestServiceImpl不实现接口可正常运行。**

下图为jdk动态代理产生：

![jdk动态代理](https://github.com/ZephXu07/IMG/raw/master/JDKDynamicProxy.png)

下图为cglib动态代理产生：

![cglib动态代理](https://github.com/ZephXu07/IMG/raw/master/CGLIBDynamicProxy.png)

-   AOP原理:动态代理.

-   -   如果目标对象有接口,那么默认采用JDK动态代理(基于接口(代理类和目标类实现共同的接口.)).
-   -   如果目标对象
        没有接口,那么采用Cglib动态代理(基于继承(代理类是目标类的子类)).
-   -   推荐,使用JDK动态代理
        .也就是我们推荐采用面向接口编程.面向抽象编程.
-   [自我笔记](https://zephxu07.github.io/2019/10/02/动态代理笔记/)

#### [](#6-、-Override "(6)、@Override")(6)、@Override {#6-、-Override}

-   如果类实现接口,实现方法时,对于编译器级别1.5,方法上不允许增加这个注解.(在1.5级别时,类对接口的实现不叫继承.)
-   对于1.6以上级别就可以增加这个注解.类继承类,类实现接口,都可以
    看做方法的重写.
-   重写规则：
-   -   方法名与形参列表必须一致。
    -   -   子类的权限修饰符必须要大于或者等于父类的权限修饰符。
    -   -   子类的返回值类型必须要小于或者 等于父类的返回值类型
    -   -   子类抛出的异常类型要小于或者等于父类抛出的异常类型。
            Exception(最坏) RuntimeException(小坏)

#### [](#7-、jdbc-properties属性文件 "(7)、jdbc.properties属性文件")(7)、jdbc.properties属性文件 {#7-、jdbc-properties属性文件}

-   键值对,不要留空格.

#### [](#8-、log4j-properties-默认名称，放resources下 "(8)、log4j.properties 默认名称，放resources下")(8)、log4j.properties 默认名称，放resources下 {#8-、log4j-properties-默认名称，放resources下}

+--------------------------------------+--------------------------------------+
|     1234567891011                    |     # DEBUG < INFO < WARN < ERROR <  |
|                                      | FATAL（严重错误）log4j.rootLogger=DEBUG, s |
|                                      | tdout# 级别之上全部打印，开发使用DEBUG，stdout随意取， |
|                                      | 但需要和下文相同log4j.appender.stdout=org.ap |
|                                      | ache.log4j.ConsoleAppender# 打印到控制台lo |
|                                      | g4j.appender.stdout.Target=System.ou |
|                                      | t# out黑色，error红色log4j.appender.stdou |
|                                      | t.layout=org.apache.log4j.PatternLay |
|                                      | outlog4j.appender.stdout.layout.Conv |
|                                      | ersionPattern=%d{yyyy-MM-dd HH:mm:ss |
|                                      |  S} %5p %c:%l - %m%n                 |
+--------------------------------------+--------------------------------------+

-   BUG：

    **SLF4J: No SLF4J providers were found.**

-   [原因及解决方法](https://blog.csdn.net/u010325193/article/details/84896420)

-   -   **其中3.SLF4J和Log4j的配合使用的jar包可更新至最新，注意log4j的配合版本**

#### [](#9-、自定义监听器-StartSystemListener "(9)、自定义监听器:StartSystemListener")(9)、自定义监听器:StartSystemListener {#9-、自定义监听器-StartSystemListener}

#### [](#10-、悲观锁和乐观锁 "(10)、悲观锁和乐观锁")(10)、悲观锁和乐观锁 {#10-、悲观锁和乐观锁}

#### [](#11-、url扩展名称 "(11)、url扩展名称")(11)、url扩展名称 {#11-、url扩展名称}

+--------------------------------------+--------------------------------------+
|     12                               |     <url-pattern>*.htm</url-pattern> |
|                                      | <!--主要用于页面跳转，WEB-IF下的jsp--><url-patt |
|                                      | ern>*.do</url-pattern><!--主要用于业务逻辑处理 |
|                                      | -->                                  |
+--------------------------------------+--------------------------------------+

#### [](#12-、生产环境的模拟 "(12)、生产环境的模拟")(12)、生产环境的模拟 {#12-、生产环境的模拟}

将本地开发环境和生产环境保持一致，可以提前发现用户在使用时所发生的问题，如果环境不一样，有些问题就无法提前暴露出来，不好解决。

##### [](#a、80端口的作用（http） "a、80端口的作用（http）")a、80端口的作用（http） {#a、80端口的作用（http）}

-   输入网址时会默认加上端口，http为80，https为443

-   用作web服务（https 443）的默认访问端口，Tomcat服务器默认的端口为8080
    (安全协议8443），**可以修改server.xml文件进行修改。**（推荐1024到65532）[端口号范围](https://www.cnblogs.com/happykoukou/p/6655852.html)

`<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" URIEncoding="UTF-8" />`

-   80端口可能被其他软件占用，使用时，必须将占用端口的软件关闭。

![ChangePort](https://github.com/ZephXu07/IMG/raw/master/ChangePort.png)

##### [](#b、Web应用不通过web项目名称也可以访问 "b、Web应用不通过web项目名称也可以访问")b、Web应用不通过web项目名称也可以访问 {#b、Web应用不通过web项目名称也可以访问}

![Application
Context](https://github.com/ZephXu07/IMG/raw/master/ApplicationContex.png)

##### [](#c、Web应用通过域名访问 "c、Web应用通过域名访问")c、Web应用通过域名访问 {#c、Web应用通过域名访问}

-   修改域名解析，通过指定的域名访问web应用，尽量模拟真实的生产环境

-   修改c:\\Windows\\System32\\drivers\\etc\\hosts文件就可以了

-   `127.0.0.1    www.zephxu.com`

##### [](#d、测试 "d、测试")d、测试 {#d、测试}

![测试结果](https://github.com/ZephXu07/IMG/raw/master/TestPort.png)

#### [](#13-、相对路径和绝对路径 "(13)、相对路径和绝对路径")(13)、相对路径和绝对路径 {#13-、相对路径和绝对路径}

##### [](#a、绝对路径 "a、绝对路径")a、绝对路径 {#a、绝对路径}

-   不可改变的路径称之为绝对路径

-   本地路径：以盘符开始的路径称之为绝对路径, c:/test/test.html

-   网络路径：以协议，域名,端口号所组合的路径为绝对路径

-   -   [http://localhost:8080/atcrowdfunding/image/xxx.jpg](http://localhost:8080/atcrowdfunding/image/xxx.jpg)
-   -   [http://www.xxx.com/test/test.com](http://www.xxx.com/test/test.com)

##### [](#b、相对路径 "b、相对路径:")b、相对路径: {#b、相对路径}

-   可以改变的路径

-   默认的相对路径需要一个参考的位置，取值为当前资源的**访问**路径

##### [](#c、路径以斜杠开头 "c、路径以斜杠开头")c、路径以斜杠开头 {#c、路径以斜杠开头}

-   路径以斜杠开头，也是相对路径，但是参考的位置和默认的相对路径不一样

-   前台路径（img， css， js, form）

-   -   参考的位置是服务器的根路径
-   -   `response.sendRedirect(request.getContextPath()+"/xxx.jsp");  //前台路径`
-   后台路径( java, xml )

-   -   参考的位置是web应用的根路径
-   -   `request.getRequestDispatcher("/xxx.jsp").forward(req,resp);  //后台路径`

+--------------------------------------+--------------------------------------+
|     123456                           |     <%--<a href="/test.do">test</a>T |
|                                      | omcat/webapps/ROOT下--%><%--<a href=" |
|                                      | http://www.zephxu.com/test.do">test< |
|                                      | /a>绝对路径--%><%--<a href="${pageContex |
|                                      | t.request.contextPath}/test.do">test |
|                                      | </a>路径以斜杠开头的前台路径--%><%--<jsp:include |
|                                      |  page="/test.jsp"></jsp:include>路径以斜 |
|                                      | 杠开头的前台路径--%><%--<img src="">路径以斜杠开头的 |
|                                      | 前台路径--%><%--response.sendRedirect(re |
|                                      | quest.getContextPath()+"/xxx.jsp");  |
|                                      |  //前台路径--%><%--<%@ page contentType= |
|                                      | "text/html;charset=UTF-8" language=" |
|                                      | java" isELIgnored="false" errorPage= |
|                                      | "/error.jsp" %>后台路径，不加“/”相对访问路径查找（访问 |
|                                      | 此jsp的请求路径），加“/”则是此jsp的相对路径--%> |
+--------------------------------------+--------------------------------------+

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
-   [Java](javascript:void(0))

[**](javascript:;)

[**](javascript:;) [**](javascript:;) [**](javascript:;)
[**](javascript:;) [**](javascript:;) [**](javascript:;)
[**](javascript:;) [**](javascript:;)

[**](javascript:;)

扫一扫，分享到微信

![微信分享二维码](//pan.baidu.com/share/qrcode?url=http://yoursite.com/2019/10/30/Practice-Project/)

[**](/2019/11/14/Linux-Notes/)

Linux Notes

[](/2019/10/15/SSM框架整合/)

SSM框架整合

**

[**](javascript:void(0))

**

**

1.  [1. 使用SSM框架开发众筹网站](#使用SSM框架开发众筹网站)
    1.  [1.1. 一、项目第一天计划](#一、项目第一天计划)
        1.  [1.1.1. 1、 课件目录结构介绍](#1、-课件目录结构介绍)
        2.  [1.1.2.
            2、互联网金融项目背景，概念介绍](#2、互联网金融项目背景，概念介绍)
        3.  [1.1.3. 3、项目管理与环境搭建](#3、项目管理与环境搭建)
            1.  [1.1.3.1. (1)、尚筹网项目构成](#1-、尚筹网项目构成)
                1.  [1.1.3.1.1. a、项目范围](#a、项目范围)
                2.  [1.1.3.1.2. b、人员组织结构](#b、人员组织结构)
                3.  [1.1.3.1.3.
                    c、项目周期（时间进度）](#c、项目周期（时间进度）)

            2.  [1.1.3.2.
                (2)、尚筹网项目需求分析](#2-、尚筹网项目需求分析)
            3.  [1.1.3.3. (3)、尚筹网项目设计](#3-、尚筹网项目设计)
            4.  [1.1.3.4. (4)、尚筹网 项目开发](#4-、尚筹网-项目开发)
                1.  [1.1.3.4.1. (a)、项目环境搭建
                    （非常重要）](#a-、项目环境搭建-（非常重要）)
                    1.  [1.1.3.4.1.1.
                        (i)、创建Web项目（生成基本的web应用文件结构）（普通）](#i-、创建Web项目（生成基本的web应用文件结构）（普通）)
                    2.  [1.1.3.4.1.2.
                        (ii)、修改开发工具的相关配置](#ii-、修改开发工具的相关配置)
                    3.  [1.1.3.4.1.3.
                        (iii)、增加基础框架的类库及相应配置文件](#iii-、增加基础框架的类库及相应配置文件)
                    4.  [1.1.3.4.1.4.
                        (iv)、增加项目基础JAVA代码（包，接口，类）](#iv-、增加项目基础JAVA代码（包，接口，类）)

                2.  [1.1.3.4.2. (b)、项目代码开发](#b-、项目代码开发)

        4.  [1.1.4. 4、Maven项目模块划分](#4、Maven项目模块划分)
            1.  [1.1.4.1. (1)、模块划分](#1-、模块划分)
            2.  [1.1.4.2. (2)、模块关系](#2-、模块关系)
            3.  [1.1.4.3. (3)、注意事项](#3-、注意事项)

        5.  [1.1.5. 5、项目环境搭建细节](#5、项目环境搭建细节)
            1.  [1.1.5.1. (1)、监听器：](#1-、监听器：)
                1.  [1.1.5.1.1. a、](#a、)
                2.  [1.1.5.1.2.
                    b、ServletContextListenner监听器接口：](#b、ServletContextListenner监听器接口：)
                3.  [1.1.5.1.3.
                    c、ServletContextAttributeListener：](#c、ServletContextAttributeListener：)
                4.  [1.1.5.1.4.
                    d、HttpSessionListener](#d、HttpSessionListener)
                5.  [1.1.5.1.5.
                    e、HttpSessionAttributeListener](#e、HttpSessionAttributeListener)
                6.  [1.1.5.1.6.
                    f、ServletRequestListener](#f、ServletRequestListener)
                7.  [1.1.5.1.7.
                    g、ServletRequestAttributeListener](#g、ServletRequestAttributeListener)

            2.  [1.1.5.2. (2)、字符编码过滤器](#2-、字符编码过滤器)
                1.  [1.1.5.2.1.
                    a、Web开发:javax.servlet.Filter](#a、Web开发-javax-servlet-Filter)
                2.  [1.1.5.2.2. b、过滤器过滤规则:](#b、过滤器过滤规则)
                3.  [1.1.5.2.3.
                    c、项目中解决乱码问题](#c、项目中解决乱码问题)
                    1.  [1.1.5.2.3.1.
                        i、POST：字符编码过滤器只能解决POST请求乱码问题.不能解决GET请求乱码](#i、POST：字符编码过滤器只能解决POST请求乱码问题-不能解决GET请求乱码)
                    2.  [1.1.5.2.3.2. ii、GET:
                        在Tomcat/conf/server.xml中设置编码.](#ii、GET-在Tomcat-conf-server-xml中设置编码)
                    3.  [1.1.5.2.3.3.
                        iii、项目开发注意事项:](#iii、项目开发注意事项)

            3.  [1.1.5.3. (3)、核心控制器](#3-、核心控制器)
                1.  [1.1.5.3.1. a、注意事项](#a、注意事项)
                2.  [1.1.5.3.2.
                    b、servlet的url-pattern匹配规则：](#b、servlet的url-pattern匹配规则：)

            4.  [1.1.5.4.
                (4)、Spring、springmvc相关配置](#4-、Spring、springmvc相关配置)
                1.  [1.1.5.4.1. a、spring：](#a、spring：)
                2.  [1.1.5.4.2. b、springmvc：](#b、springmvc：)
                3.  [1.1.5.4.3. c、创建包结构](#c、创建包结构)

        6.  [1.1.6. 6、注意问题](#6、注意问题)
            1.  [1.1.6.1. (1)、零容忍.](#1-、零容忍)
            2.  [1.1.6.2.
                (2)、mybatis框架加载核心配置文件,设置的别名查找不到.](#2-、mybatis框架加载核心配置文件-设置的别名查找不到)
            3.  [1.1.6.3.
                (3)、Service层实现类上没有增加@Service注解,导致Controller无法注入service对象.](#3-、Service层实现类上没有增加-Service注解-导致Controller无法注入service对象)
            4.  [1.1.6.4.
                (4)、@Autowired进行依赖注入方式：](#4-、-Autowired进行依赖注入方式：)
                1.  [1.1.6.4.1. a、](#a、-1)
                2.  [1.1.6.4.2. b、](#b、)
                3.  [1.1.6.4.3. c、](#c、)
                4.  [1.1.6.4.4. d、](#d、)

            5.  [1.1.6.5. (5)、AOP动态代理相关](#5-、AOP动态代理相关)
            6.  [1.1.6.6. (6)、@Override](#6-、-Override)
            7.  [1.1.6.7.
                (7)、jdbc.properties属性文件](#7-、jdbc-properties属性文件)
            8.  [1.1.6.8. (8)、log4j.properties
                默认名称，放resources下](#8-、log4j-properties-默认名称，放resources下)
            9.  [1.1.6.9.
                (9)、自定义监听器:StartSystemListener](#9-、自定义监听器-StartSystemListener)
            10. [1.1.6.10. (10)、悲观锁和乐观锁](#10-、悲观锁和乐观锁)
            11. [1.1.6.11. (11)、url扩展名称](#11-、url扩展名称)
            12. [1.1.6.12. (12)、生产环境的模拟](#12-、生产环境的模拟)
                1.  [1.1.6.12.1.
                    a、80端口的作用（http）](#a、80端口的作用（http）)
                2.  [1.1.6.12.2.
                    b、Web应用不通过web项目名称也可以访问](#b、Web应用不通过web项目名称也可以访问)
                3.  [1.1.6.12.3.
                    c、Web应用通过域名访问](#c、Web应用通过域名访问)
                4.  [1.1.6.12.4. d、测试](#d、测试)

            13. [1.1.6.13.
                (13)、相对路径和绝对路径](#13-、相对路径和绝对路径)
                1.  [1.1.6.13.1. a、绝对路径](#a、绝对路径)
                2.  [1.1.6.13.2. b、相对路径:](#b、相对路径)
                3.  [1.1.6.13.3. c、路径以斜杠开头](#c、路径以斜杠开头)

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
