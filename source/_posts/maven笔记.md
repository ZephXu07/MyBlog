---
title: maven笔记
date: 2020-01-23 23:21:29
tags: [笔记, maven]
---

maven笔记 
=========

**Maven**项目管理

[siki](http://www.sikiedu.com/course/284/material/14783/download)

**Maven**是什么？
Maven是Apache下的项目管理工具，它由纯Java语言开发，可以帮助我们更方便的管理和构建Java项目。

**为什么要使用Maven？**

1、 jar包管理：

a)
从Maven中央仓库获取标准的规范的jar包以及相关依赖的jar包，避免自己下载到错误的jar包；

b) 本地仓库统一管理jar包，使jar包与项目分离，减轻项目体积。

2、 maven是跨平台的可以在window、linux上使用。

3、 清晰的项目结构；

4、 多工程开发，将模块拆分成若干工程，利于团队协作开发。

5、
一键构建项目：使用命令可以对项目进行一键构建，操作系统中无需安装eclipse和tomcat。

**我能从这门课中学到什么？**

1、 了解Maven和它的优点；

2、 掌握Maven项目配置、命令；

3、 使用Maven+Tomcat进行热部署；

4、 使用Maven集成SSM框架；

5、 使用Maven分模块开发；

6、 学会Maven私服的搭建和使用；

[Maven从哪获取？](http://maven.apache.org/download.cgi)

**开始学习Maven项目管理工具**

Part.1 Maven入门：

1、 下载、安装、配置环境变量Maven；

a) 安装JDK 1.8；

b) 配置环境变量；

 i. win + r 打开运行窗口 或者 进入cmd命令窗口；

 ii. 输入sysdm.cpl打开系统属性 -\> 高级 -\> 环境变量；

 iii. 新建系统变量，变量名：MAVEN\_HOME，变量值：Maven安装路径；

 iv. 在Path下追加一条属性指向Maven的bin目录 %MAVEN\_HOME%/bin

2、 Maven的优点：

a) jar包管理：依赖管理

 i.
从Maven中央仓库获取标准的规范的jar包以及相关依赖的jar包，避免自己下载到错误的jar包；

 ii. 本地仓库统一管理jar包，使jar包与项目分离，减轻项目体积。

![1](https://github.com/ZephXu07/IMG/raw/master/1.png?raw=true)



(Maven项目获取jar包的方式)

 iii. Maven项目通过坐标的方式从本地仓库获取jar包；

\\1. 坐标：由公司/组织名(groupId) + 项目名/子项目名(artifactId) +
版本号(version)组成；

\\2. 本地仓库：存放很多jar包，供Maven项目使用；

\\3.
Maven通过建立本地仓库索引，可以快速的找到符合要求的jar包，从而解决效率问题；

\\4. 多个Maven项目都可以从本地仓库获取jar包；

\\5. 设置本地仓库：maven根目录 -\> conf -\>
settings.xml，将localRepository标签中的路径替换成自己本地仓库的路径；

 iv. Maven三种仓库概念：本地仓库、远程仓库、中央仓库

![2](https://github.com/ZephXu07/IMG/raw/master/2.png?raw=true)

(Maven三种仓库概念)

 v. 设置阿里云Maven仓库镜像：

\\1. 在settings.xml文件中的mirrors下添加mirror标签；

```xml
<mirror>
	<id>alimaven</id>
	<name>aliyunmaven</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public/</url>			
	<mirrorOf>central</mirrorOf>
</mirror>                            
```

b) maven由纯Java语言开发，是跨平台的可以在window、linux、mac上使用。

c) 清晰的项目结构；

d)
使用Maven将大型项目按照模块拆分成若干工程，不同的团队维护各自的工程，可大大的提升开发效率；

 i. 大型商城项目按业务分成商品管理、用户管理、订单管理等等模块。

![3](https://github.com/ZephXu07/IMG/raw/master/3.png?raw=true)

(大型项目，分模块开发)

 ii.
中小型项目按照传统项目分为Web、Service、Dao层，依照员工自身的业务能力分配工作。

![4](https://github.com/ZephXu07/IMG/raw/master/4.png)

(中小型项目，分层开发)

e)
一键构建项目：使用命令可以对项目进行一键构建，操作系统中无需安装eclipse和tomcat。

3、 Maven常用命令：

a) clean： 清理，编译后的目录；

b) compile： 编译，只编译main目录，不编译test中的代码；

c) test-compile：编译test目录中的代码；

d) test： 运行test里边的代码；

e) package： 打包

 i. java项目-\>打成jar包；

 ii. web项目-\>打成war包；

f)
install：发布项目到本地仓库，用在打jar包上，打成jar包可以被其他项目使用；

g) tomcat:run：一键构建项目；

4、 Maven命令的生命周期：

a) Clean 生命周期：clean；

b) Default 生命周期：compile、test-compile、test、package、install

c) Site 生命周期：site命令，生成项目描述文档静态页；

d) 不同的生命周期可以一起执行，例如先clean 再compile；

5、 Maven命令的执行顺序：

a) 在相同生命周期中的命令才会受执行顺序的影响；

b) Default生命周期中的命令执行顺序：

compile \<- test-compile \<- test \<- package \<- install；

Part.2 Maven入门程序：

Ø 入门程序：

1、 创建Maven项目；

2、 在src -\> main -\> webapp下创建WEB-INF目录，并在目录下创建web.xml；

3、 修改Maven默认编译级别：

a) 全局编译级别 -\> 修改settings.xml

b) 项目级别修改 -\> 项目对应的pom.xml

4、 在Java Resourcese -\> src/main/java下写代码，创建包和Servlet；

5、 添加servlet-api：

6、 在servlet-api中添加scope标签，值为：proviede；

a)
如果不加此标签有很大几率报错，因为tomcat中也有servlet-api的包导致冲突；

7、
运行：发生错误，原因是maven默认使用tomcat6.xx，不支持@WebServle注解；

a) 解决方案1：需要去web.xml中配置Servlet;

b) 解决方案2：配置高版本tomcat插件；

8、 最后测试，启动服务，在地址栏输入请求，显示结果；

Ø 使用tomcat7插件运行项目；

Ø
Scope依赖作用域也可称作依赖范围：maven中的依赖，会根据程序所处的阶段和场景发生变化，所以maven用scope属性来做限制；

a) compile（默认值）：在编译、运行、测试、打包都有效；

b) provided：编译、测试时有效，运行、打包无效；

c) test：仅在测试时有效；

d) runtime：测试、运行、打包时有效；

e)
system：不推荐使用，使用system作用域不会去本地仓库寻找依赖，要指定本地路径；

![5](https://github.com/ZephXu07/IMG/raw/master/5.png)

（依赖关系中作用域说明）

**Part.3 Maven 3.5.4 + tomcat 8.5.32** **热部署：**

 热部署：在tomcat运行时将项目部署上去；

1、 开启tomcat热部署：

a) 修改tomcat -\> conf-\> tomcat-users.xml 配置文件；

b) 在tomcat-users标签中加入以下代码：

```xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="joey" password="123123" roles="manager-gui, manager-script"/> 
```

c) 启动tomcat；

d) 修改项目中pom.xml，在tomcat7的插件上添加以下代码：

```xml
<configuration> 
	<url>http://localhost:8080/manager/text</url> 
	<username>joey</username> 
	<password>123123</password>
</configuration>          |
```

e) 右键项目-\> run as -\> maven build…
在goals中使用tomcat7:deploy或tomcat7:redeploy来进行热部署；

 i. tomcat7:deploy，第一次部署时使用。

 ii. tomcat7:redeploy，非第一次部署时使用。

f) 部署完毕，打开浏览器测试；

**Part.4 Maven** **整合SSM框架 ：**

1、 Maven+SSM框架整合；

a) 加入SSM框架所需的依赖；

b) 配置插件；

c) 导入SSM框架所需配置文件；

d) 配置Maven Resources资源放行：

 i.
因为Maven会把src/main/java下的\*.java文件文件编译放到target/classes目录目录中，但这目录中的其他文件会被忽略；

 ii. Mybatis Mapper映射文件也要放在src/main/java下，所以不能忽略；

 iii. 因此我们需要对src/main/java下的配置文件进行过滤，不能被忽略；

 iv. 利用Maven中的Resources标签可以进行配置；

2、 测试；

a) 新建名为User的bean对象，有username，password俩字段；

b) 新建login.jsp，可以输入用户名和密码，通过表单提交到后台；

c) 后台接受用户名和密码，跳转页面，并显示；

3、 读取数据库显示游戏列表；

a) 导入item\_info表；

b) 在login.jsp中增加button，点击后跳转页面，显示列表；

**Part.5 Maven** **模块化开发 ：**

![6](https://github.com/ZephXu07/IMG/raw/master/6.png)

（Maven模块化开发项目依赖关系）

Ø 需求：将Maven-SSM项目以层为单位拆分，按模块开发；

1、 创建父项目，在父项目中加入依赖；

2、 创建mapper层子项目继承父项目；

3、 子项目可以继承父项目的依赖；

4、 利用junit测试mapper模块项目；

5、 Maven的依赖传递，与依赖版本管理；

a) 依赖传递：添加依赖的jar包如果还依赖其他jar包，则在添加时会一起引入；

b) 依赖冲突：Base-project由3个子项目组成，A-project依赖Tools.jar
1.0版本，C-project依赖Tools.jar
2.0版本，根据依赖传递机制，Base-project将同时依赖Tools.jar两个版本，但这造成了冲突。根据路径最近获胜策略，该项目最终依赖Tools.jar
1.0，导致C-project无法调用getAll方法从而报错，因此我们要手动选择一个适合项目的版本。

![7](https://github.com/ZephXu07/IMG/raw/master/7.png)

（Maven模块化开发项目依赖关系）

c) 解决依赖冲突的办法：

 i. 直接声明：直接添加Tools.jar 2.0依赖；

 ii.
排除：使用`<dependency>`标签中的`<exclusions>`标签排除A-project中的Tools.jar
1.0依赖；

 iii. 依赖管理，版本锁定：`<dependencyManagement>`

\\1.
`<dependencyManagement>`是依赖管理，该标签下添加的`<dependencies>`可以声明依赖，但是不会引入jar包；

\\2.
只有声明在`<project>`标签下`<dependencies>`中的依赖才会被引用到项目中；

\\3.
在`<dependencyManagement>`下添加jar包坐标后，`<project>`标签下`<dependencies>`标签的版本号可以忽略不写；

\\4.
`< properties>`标签可以自定义版本号，用el表达式赋值给`<version>`标签；

\\5. 统一管理jar包版本，修改方便；

6、 创建scervice模块项目，利用junit测试service模块项目；

7、 依赖作用域对依赖传递的影响；

8、 创建controller模块项目，运行程序；

**Part.6 Maven** **远程仓库Nexus（私服） ：**

Ø Nexus获取与配置：

1、 下载Nexus
[点击我下载](https://www.sonatype.com/download-oss-sonatype?hsCtaTracking=920dd7b5-7ef3-47fe-9600-10fecad8aa32|f59d5f10-099f-4c66-a622-0254373f4a92)

2、 Nexus安装，解压缩到本地即可；

3、
Nexus安装目录下nexus-3.14.0-04/etc/nexus-default.properties配置表中可以修改以下属性：

a) application-host : Nexus服务监听的主机；

b) application-port: Nexus服务监听的端口；

c) nexus-context-path : Nexus服务的上下文路径；

4、 Nexus服务配置和启动：

a) 以管理员身份运行cmd -\>
进入到nexus安装目录../nexus-3.14.0-04/bin目录下；

b) 在cmd中运行 nexus.exe/install 可以安装nexus服务；

c) 在cmd中运行 nexus.exe/start 可以启动nexus服务；

d) 在cmd中运行 nexus.exe/stop 可以停止nexus服务；

5、 登录Nexus：

a)
启动服务后，根据nexus-default.properties的配置进行登录，如果没有修改，可以[点击此处](http://localhost:8081)来登录；

b) 默认用户名是admin，密码是admin123；

6、 仓库类型：nexus有多种仓库类型：

![8](https://github.com/ZephXu07/IMG/raw/master/8.png)

（Nexus仓库类型介绍）



Ø Nexus使用：

需求：将项目中的mapper.jar包提交到远程仓库中，
使service项目从远程仓库获取；

² 上传jar包到远程仓库；

1、 在Maven的 setting.xml中配置nexus访问权限；

2、 在项目的pom.xml中配置nexus仓库位置；

3、 以上2个配置标签中的id要一致；

4、 使用deploy命令将项目打包，发布到nexus中；

5、 检查仓库中是否有上传好的jar包；

² 从远程仓库下载jar包：

1、 使用profiles标签在Maven的setting.xml中配置仓库位置；

2、 激活profiles标签，使它发生作用；

3、 如果之前打包了，删除本地仓库下的mapper.jar；

4、 关闭mapper子项目，让service子项目依赖mapper.jar包；

5、 更新项目，从远程仓库中获取mapper.jar；

² 使用自定义用户和自定义仓库进行上传和下载jar包：

1、 建议先将管理员密码修改；

2、 在Roles中可以增加用户权限组，里边可以自定义用户权限；

3、 在Users中可以增加用户，分配设置好的权限；

4、 在Repositories中新建仓库；

a) name：仓库名称；

b) version pollcy：版本策略；

 i. Release：发行版；

 ii. Snapshot：快照版；

 iii. Mixed：混合模式；

c) Layout pollcy：布局策略；

 i. Strict：严格；

 ii. Permissive：宽松；

d) Deployment pollcy：部署策略；

 i. Allow redeploy：允许重新部署；

 ii. Disable redeploy：禁止重新部署；

 iii. Read-only：只读；

5、 修改配置，将jar包上传到自定义仓库，然后从自定义仓库下载jar包；a