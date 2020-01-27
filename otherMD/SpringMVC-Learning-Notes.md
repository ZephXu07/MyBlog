[![](/assets/img/HeadFish.jpg)](/)

[ZephXu07](/)
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

ZephXu07
========

[**](https://github.com/ZephXu07 "github")
[**](https://weibo.com/5409078656/profile?rightmod=1&wvr=6&mod=personinfo&is_all=1 "weibo")
[**](https://space.bilibili.com/14445452 "bilibili")

-   [主页](/)
-   [笔记](/tags/笔记/)
-   [归档](/archives/index.html)

SpringMVC Learning Notes
========================


 [阅读数: 次   ](javascript:void(0);)
[**2019-10-05](/2019/10/05/SpringMVC-Learning-Notes/)

[](#SpringMVC-个人学习笔记 "SpringMVC 个人学习笔记")SpringMVC 个人学习笔记
==========================================================================

（[学习视频](https://www.bilibili.com/video/av47953244)，[学习资料（提取码3b45）](https://pan.baidu.com/s/1Tn7T5c0wzvv5apYl5G0mdQ)）

（过于正式标准全部是学习资料自带的……）

[](#part1、三层架构和MVC "part1、三层架构和MVC")part1、三层架构和MVC
--------------------------------------------------------------------

### [](#一、三层架构 "一、三层架构")一、三层架构

1、开发服务器端程序，一般都基于两种形式，一种C/S架构程序，一种B/S架构程序
；

2、使用Java语言基本上都是开发B/S架构的程序，B/S架构又分成了三层架构

3、三层架构

a)
表现层：WEB层，用来和客户端进行数据交互的。表现层一般会采用MVC的设计模型
；

b) 业务层：处理公司具体的业务逻辑的 ；

c) 持久层：用来操作数据库的。

### [](#二、MVC模型 "二、MVC模型")二、MVC模型

1、MVC全名是Model View Controller 模型视图控制器，每个部分各司其职；

2、Model：数据模型，JavaBean的类，用来进行数据封装；

3、View：指JSP、HTML用来展示数据给用户 ；

4、Controller：用来接收用户的请求，整个流程的控制器。用来进行数据校验等。

![Structure](https://github.com/ZephXu07/IMG/raw/master/Structure.bmp)

[](#part2、SpringMVC的入门案例 "part2、SpringMVC的入门案例")part2、SpringMVC的入门案例
--------------------------------------------------------------------------------------

### [](#一、SpringMVC的概述 "一、SpringMVC的概述")一、SpringMVC的概述

#### [](#1、SpringMVC的概述 "1、SpringMVC的概述")1、SpringMVC的概述

a) 一种基于Java实现的MVC设计模型的请求驱动类型的轻量级WEB框架；

b) MVC属于SpringFrameWork的后续产品，已经融合在Spring Web
Flow里面，Spring 框架提供 了构建 Web 应用程序的全功能 MVC 模块；

c) 使用 Spring 可插入的 MVC
架构，从而在使用Spring进行WEB开发时，可以选择使用Spring的
SpringMVC框架或集成其他MVC开发框架。

#### [](#2、SpringMVC在三层架构中的位置：表现层框架 "2、SpringMVC在三层架构中的位置：表现层框架")2、SpringMVC在三层架构中的位置：表现层框架

![详细结构](https://github.com/ZephXu07/IMG/raw/master/DetailedStructure.png)

#### [](#3、SpringMVC的优势 "3、SpringMVC的优势")3、SpringMVC的优势

1、清晰的角色划分（流水线）：

前端控制器（DispatcherServlet）

请求到处理器映射（HandlerMapping）

处理器适配器（HandlerAdapter）

视图解析器（ViewResolver）

处理器或页面控制器（Controller）

验证器（ Validator）

命令对象（Command 请求参数绑定到的对象就叫命令对象）

表单对象（Form Object 提供给表单展示和提交到的对象就叫表单对象）

2、分工明确，而且扩展点相当灵活，可以很容易扩展，虽然几乎不需要。

3、由于命令对象就是一个 POJO，无需继承框架特定
API，可以使用命令对象直接作为业务对象。

4、和 Spring 其他框架无缝集成，是其它 Web 框架所不具备的。

5、可适配，通过 HandlerAdapter 可以支持任意的类作为处理器。

6、可定制性，HandlerMapping、ViewResolver 等能够非常简单的定制。

7、功能强大的数据验证、格式化、绑定机制。

8、利用 Spring 提供的 Mock 对象能够非常简单的进行 Web 层单元测试。

9、本地化、主题的解析的支持，使我们更容易进行国际化和主题的切换。

10、强大的 JSP 标签库，使 JSP 编写更容易。

还有比如RESTful风格的支持、简单的文件上传、约定大于配置的契约式编程支持、基于注解的零配置支持等等。

#### [](#4、SpringMVC和Stru2的对比 "4、SpringMVC和Stru2的对比")4、SpringMVC和Stru2的对比

##### [](#共同点： "共同点：")共同点：

它们都是表现层框架，都是基于 MVC 模型编写的。 它们的底层都离不开原始
ServletAPI。 它们处理请求的机制都是一个核心控制器。

##### [](#区别： "区别：")区别：

Spring MVC 的入口是 Servlet, 而 Struts2 是 Filter 。Spring MVC
是基于方法设计的，而 Struts2 是基于类，Struts2
每次执行都会创建一个动作类。所以Spring MVC 会稍微比 Struts2 快些。
Spring MVC 使用更加简洁,同时还支持 JSR303, 处理 ajax 的请求更方便。
(JSR303 是一套 JavaBean
参数校验的标准，它定义了很多常用的校验注解，我们可以直接将这些注解加在我们
JavaBean 的属性上面，就可以在需要校验的时候进行校验了。) Struts2 的 OGNL
表达式使页面的开发效率相比 Spring MVC 更高些，但执行效率并没有比 JSTL
提升，尤其是 struts2 的表单标签，远没有 html 执行效率高。

### [](#二、SpringMVC的入门程序 "二、SpringMVC的入门程序")二、SpringMVC的入门程序

![流程图](https://github.com/ZephXu07/IMG/raw/master/FlowDiagram%20.png)

#### [](#1、创建Web工程，引入开发的jar包 "1、创建Web工程，引入开发的jar包")1、创建Web工程，引入开发的jar包

##### [](#具体坐标如下 "具体坐标如下")具体坐标如下

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819202122232425262728293031323334353637383940</code></pre></td>
<td align="left"><pre><code>&lt;properties&gt;    &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;    &lt;maven.compiler.source&gt;1.8&lt;/maven.compiler.source&gt;    &lt;maven.compiler.target&gt;1.8&lt;/maven.compiler.target&gt;    &lt;spring.version&gt;5.2.0.RELEASE&lt;/spring.version&gt;  &lt;/properties&gt;  &lt;dependencies&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-context&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-web&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;dependency&gt;      &lt;groupId&gt;org.springframework&lt;/groupId&gt;      &lt;artifactId&gt;spring-webmvc&lt;/artifactId&gt;      &lt;version&gt;${spring.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api --&gt;    &lt;dependency&gt;      &lt;groupId&gt;javax.servlet&lt;/groupId&gt;      &lt;artifactId&gt;javax.servlet-api&lt;/artifactId&gt;      &lt;version&gt;4.0.1&lt;/version&gt;      &lt;scope&gt;provided&lt;/scope&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api --&gt;    &lt;dependency&gt;      &lt;groupId&gt;javax.servlet.jsp&lt;/groupId&gt;      &lt;artifactId&gt;javax.servlet.jsp-api&lt;/artifactId&gt;      &lt;version&gt;2.3.3&lt;/version&gt;      &lt;scope&gt;provided&lt;/scope&gt;    &lt;/dependency&gt;&lt;/dependencies&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#2、配置核心的控制器（配置DispatcherServlet） "2、配置核心的控制器（配置DispatcherServlet）")2、配置核心的控制器（配置DispatcherServlet）

##### [](#在web-xml配置文件中核心控制器DispatcherServlet "在web.xml配置文件中核心控制器DispatcherServlet")在web.xml配置文件中核心控制器DispatcherServlet

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718</code></pre></td>
<td align="left"><pre><code>&lt;!-- SpringMVC的核心控制器 --&gt; &lt;servlet&gt;   &lt;servlet-name&gt;dispatcherServlet&lt;/servlet-name&gt;   &lt;servlet-class&gt;org.springframework.web.servlet.DispatcherServlet&lt;/servlet-class&gt;   &lt;!-- 配置Servlet的初始化参数，读取springmvc的配置文件，创建spring容器 --&gt;   &lt;init-param&gt;     &lt;param-name&gt;contextConfigLocation&lt;/param-name&gt;     &lt;!--给上面的DispatcherServlet类的contextConfigLocation传值，读取配置文件--&gt;     &lt;param-value&gt;classpath:SpringMVC.xml&lt;/param-value&gt;   &lt;/init-param&gt;   &lt;!--配置servlet启动时加载对象，DispatcherServlet第一次发请求时被创建--&gt;   &lt;load-on-startup&gt;1&lt;/load-on-startup&gt; &lt;/servlet&gt; &lt;servlet-mapping&gt;   &lt;servlet-name&gt;dispatcherServlet&lt;/servlet-name&gt;   &lt;url-pattern&gt;/&lt;/url-pattern&gt;   &lt;!--&quot;/&quot;发送任何请求都会经过DispatcherServlet--&gt; &lt;/servlet-mapping&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#3、编写springmvc-xml的配置文件 "3、编写springmvc.xml的配置文件")3、编写springmvc.xml的配置文件

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314</code></pre></td>
<td align="left"><pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;&lt;beans xmlns=&quot;http://www.springframework.org/schema/beans&quot;       xmlns:mvc=&quot;http://www.springframework.org/schema/mvc&quot;       xmlns:context=&quot;http://www.springframework.org/schema/context&quot;       xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot;       xsi:schemaLocation=&quot; http://www.springframework.org/schema/beans       http://www.springframework.org/schema/beans/spring-beans.xsd       http://www.springframework.org/schema/mvc       http://www.springframework.org/schema/mvc/spring-mvc.xsd       http://www.springframework.org/schema/context       http://www.springframework.org/schema/context/spring-context.xsd&quot;&gt;    &lt;!-- 配置spring创建容器时要扫描的包--&gt;    &lt;context:component-scan base-package=&quot;com.zephxu&quot;/&gt;&lt;/beans&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#4-编写index-jsp和HelloController控制器 "4. 编写index.jsp和HelloController控制器")4. 编写index.jsp和HelloController控制器

##### [](#a-index-jsp： "a)    index.jsp：")a) index.jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011</code></pre></td>
<td align="left"><pre><code>&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;SpringMVC&lt;/title&gt;&lt;/head&gt;&lt;body&gt;    &lt;h3&gt;入门程序&lt;/h3&gt;    &lt;a href=&quot;sayHello&quot;&gt;入门程序&lt;/a&gt;&lt;%--相对路径，对应com.zephxu.controller.HelloController.sayHello上的注解--%&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

##### [](#b-HelloController "b)    HelloController")b) HelloController

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678</code></pre></td>
<td align="left"><pre><code>@Controllerpublic class HelloController {    @RequestMapping(path = &quot;/sayHello&quot;)    public String sayHello() {        System.out.println(&quot;Hello SpringMVC&quot;);        return &quot;success&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

**SpringMVC默认规则：return
"success"字符串默认为打开新的success.jsp.页面，即5、的操作**

**前提是开启下面的配置**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678</code></pre></td>
<td align="left"><pre><code>&lt;!--视图解析器--&gt;    &lt;bean id=&quot;internalResourceViewResolver&quot; class=&quot;org.springframework.web.servlet.view.InternalResourceViewResolver&quot;&gt;        &lt;property name=&quot;prefix&quot; value=&quot;/WEB-INF/pages/&quot;/&gt;&lt;!--文件所在目录--&gt;        &lt;property name=&quot;suffix&quot; value=&quot;.jsp&quot;/&gt;&lt;!--后缀--&gt;        &lt;!--前后缀连接成页面的文件--&gt;    &lt;/bean&gt;&lt;!--    SpringMVC注解支持--&gt;    &lt;mvc:annotation-driven/&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#5、在WEB-INF目录下创建pages文件夹，编写success-jsp的成功页面 "5、在WEB-INF目录下创建pages文件夹，编写success.jsp的成功页面")5、在WEB-INF目录下创建pages文件夹，编写success.jsp的成功页面

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789</code></pre></td>
<td align="left"><pre><code>&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;Title&lt;/title&gt;&lt;/head&gt;&lt;body&gt;        &lt;h3&gt;入门成功&lt;/h3&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

#### [](#6、启动Tomcat服务器，进行测试 "6、启动Tomcat服务器，进行测试")6、启动Tomcat服务器，进行测试

### [](#三、入门案例的执行过程分析 "三、入门案例的执行过程分析")三、入门案例的执行过程分析

#### [](#1、入门案例的执行流程 "1、入门案例的执行流程")1、入门案例的执行流程

a)
当启动Tomcat服务器的时候，因为配置了load-on-startup标签，所以会创建DispatcherServlet对象，
就会加载springmvc.xml配置文件

b) 开启了注解扫描，那么HelloController对象就会被创建

c).
从index.jsp发送请求，请求会先到达DispatcherServlet核心控制器，根据配置@RequestMapping注解
找到执行的具体方法

d)
根据执行方法的返回值，再根据配置的视图解析器，去指定的目录下查找指定名称的JSP文件

e) Tomcat服务器渲染页面，做出响应

![简单流程](https://github.com/ZephXu07/IMG/raw/master/ProcessOfIntroductoryCase.png)

![详细流程0](https://github.com/ZephXu07/IMG/raw/master/DetailedFlow0.png)

#### [](#2、入门案例中的组件分析 "2、入门案例中的组件分析")2、入门案例中的组件分析

##### [](#a-DispatcherServlet：前端控制器 "a)    DispatcherServlet：前端控制器")a) DispatcherServlet：前端控制器

用户请求到达前端控制器，它就相当于mvc模式中的
c，dispatcherServlet是整个流程控制的中心，由它调用其它组件处理用户的请求，dispatcherServlet的存在降低了组件之间的耦合性。

##### [](#b-HandlerMapping：处理器映射器 "b)    HandlerMapping：处理器映射器")b) HandlerMapping：处理器映射器

HandlerMapping负责根据用户请求找到Handler即处理器，SpringMVC提供了不同的映射器实现不同的映射方式，例如：配置文件方式，实现接口方式，注解方式等。

##### [](#c-Handler：处理器 "c)    Handler：处理器")c) Handler：处理器

它就是我们开发中要编写的具体业务控制器。由DispatcherServlet把用户请求转发到Handler。由Handler对具体的用户请求进行处理。

##### [](#d-HandlAdapter：处理器适配器（转接口） "d)    HandlAdapter：处理器适配器（转接口）")d) HandlAdapter：处理器适配器（转接口）

通过HandlerAdapter对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。

##### [](#e-View-Resolver：视图解析器 "e)    View Resolver：视图解析器")e) View Resolver：视图解析器

View Resolver负责将处理结果生成View视图，View
Resolver首先根据逻辑视图名解析成物理视图名即具体的页面地址，再生成View视图对象，最后对View进行渲染将处理结果通过页面展示给用户。

##### [](#f-View：视图 "f)    View：视图")f) View：视图

SpringMVC框架提供了很多的 View
视图类型的支持，包括：jstlView、freemarkerView、pdfView
等。我们最常用的视图就是 jsp。
一般情况下需要通过页面标签或页面模版技术将模型数据通过页面展示给用户，需要由程序员根据业务需求开发具体的页面。

![流程及组件](https://github.com/ZephXu07/IMG/raw/master/DetailedFlow.png)

#### [](#3、-lt-mvc-annotation-driven-gt-说明 "3、<mvc:annotation-driven>说明")3、`<mvc:annotation-driven>`说明

在 SpringMVC 的各个组件中，处理器映射器、处理器适配器、视图解析器称为
SpringMVC 的三大组件。
使用`<mvc:annotation-driven>`自动加载RequestMappingHandlerMapping（处理映射器）和RequestMappingHandlerAdapter
（ 处 理 适 配 器 ） ， 可 用 在SpringMVC.xml 配 置 文 件 中 使 用
`<mvc:annotation-driven>`替代注解处理器和适配器的配置。

它就相当于在 xml 中配置了：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213</code></pre></td>
<td align="left"><pre><code>&lt;!-- Begin --&gt; &lt;!-- HandlerMapping --&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping&quot;/&gt; &lt;bean class=&quot;org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping&quot;/&gt; &lt;!-- HandlerAdapter --&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter&quot;/&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter&quot;/&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter&quot;/&gt; &lt;!-- HadnlerExceptionResolvers --&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.method.annotation.ExceptionHandlerExceptionResolver&quot;/&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.annotation.ResponseStatusExceptionResolver&quot;/&gt; &lt;bean class=&quot;org.springframework.web.servlet.mvc.support.DefaultHandlerExceptionResolver&quot;/&gt; &lt;!-- End --&gt;</code></pre></td>
</tr>
</tbody>
</table>

**注意：**  
一般开发中，我们都需要写上此标签（虽然从入门案例中看，我们不写也行，随着课程的深入，该标签还有具体的使用场景）。

**明确：**  
我们只需要编写处理具体业务的控制器以及视图。

### [](#四、RequestMapping注解 "四、RequestMapping注解")四、RequestMapping注解

#### [](#1、RequestMapping注解的作用是建立请求URL和处理方法之间的对应关系 "1、RequestMapping注解的作用是建立请求URL和处理方法之间的对应关系")1、RequestMapping注解的作用是建立请求URL和处理方法之间的对应关系

#### [](#2-、RequestMapping注解可以作用在方法和类上：更加清晰 "2.、RequestMapping注解可以作用在方法和类上：更加清晰")2.、RequestMapping注解可以作用在方法和类上：更加清晰

a) 作用在类上：第一级的访问目录

b) 作用在方法上：第二级的访问目录

![作用域](https://github.com/ZephXu07/IMG/raw/master/RequestMappingScope.png)

**若在类上加注解，则在请求方法时路径要加上类的注解**

c) 细节：路径可以不编写 / 表示应用的根目录开始

d)
细节：`${ pageContext.request.contextPath }`也可以省略不写，但是路径上不能写
/

#### [](#3、RequestMapping的属性 "3、RequestMapping的属性")3、RequestMapping的属性

a) path：指定请求路径的url

b) value：value属性和path属性是一样的

c) method ：指定该方法的请求方式

`@RequestMapping(value = "/sayHello", method = {RequestMethod.GET, RequestMethod.POST})`

-   超链接一般是通过get方式

d) params：指定限制请求参数的条件

-   `@RequestMapping(value = "/sayHello",params = {"username"})`对应的：`<a href="user/sayHello?username=hhhh">RequestMapping注解</a>`

-   `@RequestMapping(value = "/sayHello",params = {"username=heihei"})`对应的`<a href="user/sayHello?username=heihei">RequestMapping注解</a>`

-   还有如下：

    ![详细结果](https://github.com/ZephXu07/IMG/raw/master/DetailedResult.png)

e) headers：发送的请求中必须包含的请求头

![action](https://github.com/ZephXu07/IMG/raw/master/HeadAction.png)

![result](https://github.com/ZephXu07/IMG/raw/master/HeadResult.png)

[](#part3、请求参数的绑定 "part3、请求参数的绑定")part3、请求参数的绑定
-----------------------------------------------------------------------

### [](#一、请求参数的绑定说明 "一、请求参数的绑定说明")一、请求参数的绑定说明

#### [](#1、绑定机制 "1、绑定机制")1、绑定机制

a) 表单提交的数据都是k=v格式的 username=haha&password=123

b)
SpringMVC的参数绑定过程是把表单提交的请求参数，作为控制器中方法的参数进行绑定的

c) 要求：提交表单的name和参数的名称是相同的

#### [](#2、支持的数据类型 "2、支持的数据类型")2、支持的数据类型

a) 基本数据类型和字符串类型

b) 实体类型（JavaBean）

c) 集合数据类型（List、map集合等）

### [](#二、基本数据类型和字符串类型 "二、基本数据类型和字符串类型")二、基本数据类型和字符串类型

1、提交的表单的name和参数名称是相同的

2、区分大小写

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/parameter&quot;)public class ParameterController { @RequestMapping(&quot;/testParameter&quot;)   public String testParameter(String username, int value) {     System.out.println(&quot;执行了……&quot;);      System.out.println(&quot;用户名：&quot; + username);        System.out.println(&quot;数值：&quot; + value);        return &quot;success&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

`<a href="parameter/testParameter?username=xzf&value=19990701">请求参数绑定</a>`

### [](#三、实体类型（JavaBean） "三、实体类型（JavaBean）")三、实体类型（JavaBean）

1、提交表单的name和JavaBean中的属性名称需要一致（通过JavaBean的set方法）

2、如果一个JavaBean类中包含其他的引用类型，那么表单的name属性需要编写成：对象.属性
例如： address.name

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567</code></pre></td>
<td align="left"><pre><code>public class Account implements Serializable {    private String username;    private String password;    private Double money;    private User user;    //set(), get()方法, toString()  }</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345</code></pre></td>
<td align="left"><pre><code>public class User implements Serializable {    private int id;    private int age;    //set(), get(), toString()}</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678</code></pre></td>
<td align="left"><pre><code>&lt;form action=&quot;parameter/saveAccount&quot; method=&quot;post&quot;&gt;        姓名：&lt;input type=&quot;text&quot; name=&quot;username&quot;/&gt;&lt;br/&gt;        密码：&lt;input type=&quot;password&quot; name=&quot;password&quot;/&gt;&lt;br/&gt;        金额：&lt;input type=&quot;text&quot; name=&quot;money&quot;/&gt;&lt;br/&gt;        用户ID：&lt;input type=&quot;text&quot; name=&quot;user.id&quot;/&gt;&lt;br/&gt;        用户年龄：&lt;input type=&quot;text&quot; name=&quot;user.age&quot;/&gt;&lt;br/&gt;        &lt;input type=&quot;submit&quot; value=&quot;提交&quot;&gt;&lt;/form&gt;</code></pre></td>
</tr>
</tbody>
</table>

-   **暂时会出现中文乱码：post方式！get方式正常！**

-   配置解决中文乱码的过滤器**（在servlet配置之前）**：

    **在web.xml中配置Spring提供的过滤器类**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213</code></pre></td>
<td align="left"><pre><code>&lt;filter&gt;    &lt;filter-name&gt;characterEncodingFilter&lt;/filter-name&gt;    &lt;filter-class&gt;org.springframework.web.filter.CharacterEncodingFilter&lt;/filter-class&gt;    &lt;init-param&gt;      &lt;param-name&gt;encoding&lt;/param-name&gt;      &lt;param-value&gt;UTF-8&lt;/param-value&gt;      &lt;!-- 指定字符集 --&gt;    &lt;/init-param&gt;  &lt;/filter&gt;  &lt;filter-mapping&gt;    &lt;filter-name&gt;characterEncodingFilter&lt;/filter-name&gt;    &lt;url-pattern&gt;/*&lt;/url-pattern&gt;  &lt;/filter-mapping&gt;</code></pre></td>
</tr>
</tbody>
</table>

### [](#四、集合属性数据封装 "四、集合属性数据封装")四、集合属性数据封装

#### [](#1、List：JSP页面编写方式：list-0-属性 "1、List：JSP页面编写方式：list[0].属性")1、List：JSP页面编写方式：list[0].属性

#### [](#2、Map：map-‘key’-属性 "2、Map：map[‘key’].属性")2、Map：map[‘key’].属性

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>&lt;form action=&quot;parameter/saveAccount&quot; method=&quot;post&quot;&gt;        姓名：&lt;input type=&quot;text&quot; name=&quot;username&quot;/&gt;&lt;br/&gt;        密码：&lt;input type=&quot;password&quot; name=&quot;password&quot;/&gt;&lt;br/&gt;        金额：&lt;input type=&quot;text&quot; name=&quot;money&quot;/&gt;&lt;br/&gt;        用户ID：&lt;input type=&quot;text&quot; name=&quot;userList[0].id&quot;/&gt;&lt;br/&gt;        用户年龄：&lt;input type=&quot;text&quot; name=&quot;userList[0].age&quot;/&gt;&lt;br/&gt;        用户ID：&lt;input type=&quot;text&quot; name=&quot;userMap[&#39;xzf&#39;].id&quot;/&gt;&lt;br/&gt;        用户年龄：&lt;input type=&quot;text&quot; name=&quot;userMap[&#39;xzf&#39;].age&quot;/&gt;&lt;br/&gt;        &lt;input type=&quot;submit&quot; value=&quot;提交&quot;&gt;&lt;/form&gt;</code></pre></td>
</tr>
</tbody>
</table>

### [](#五、自定义类型转换器 "五、自定义类型转换器")五、自定义类型转换器

1、表单提交的任何数据类型全部都是字符串类型，但是后台定义Integer类型，数据也可以封装上，说明
Spring框架内部会默认进行数据类型转换。

2、如果想自定义数据类型转换，可以实现Converter的接口

 a) 自定义类型转换器

 i) 正常情况：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>&lt;form action=&quot;parameter/saveUser&quot; method=&quot;post&quot;&gt;        用户ID：&lt;input type=&quot;text&quot; name=&quot;id&quot;/&gt;&lt;br/&gt;        用户年龄：&lt;input type=&quot;text&quot; name=&quot;age&quot;/&gt;&lt;br/&gt;        用户生日：&lt;input type=&quot;text&quot; name=&quot;date&quot;&gt;&lt;br/&gt; &lt;input type=&quot;submit&quot; value=&quot;提交&quot;&gt;&lt;/form&gt;</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/saveUser&quot;)    public String saveUser(User user){        System.out.println(&quot;自定义类型转换器&quot;);        System.out.println(user);        return &quot;success&quot;;}</code></pre></td>
</tr>
</tbody>
</table>

![test0](https://github.com/ZephXu07/IMG/raw/master/Test.png)

![normalResult](https://github.com/ZephXu07/IMG/raw/master/NormalResult.png)

![ThrowTest](https://github.com/ZephXu07/IMG/raw/master/ThrowTest.png)

![ThrowResult](https://github.com/ZephXu07/IMG/raw/master/ResultThrow.png)

 ii) 使用自定义类型转换器

-   自定义类型转换器类：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819</code></pre></td>
<td align="left"><pre><code>public class StringToDateConverter implements Converter&lt;String, Date&gt; {    /**     *     * @param s 传入的值yyyy-MM-dd     * @return     */    @Override    public Date convert(String s) {        if(null != s) {            throw new RuntimeException(&quot;请传入数值&quot;);        }        DateFormat df = new SimpleDateFormat(&quot;yyyy-MM-dd&quot;);        try {            return df.parse(s);        } catch (ParseException e) {            throw new RuntimeException(&quot;数据类型转换出现错误&quot;);        }    }}</code></pre></td>
</tr>
</tbody>
</table>

-   SpringMVC.xml配置：

    <table>
    <col width="50%" />
    <col width="50%" />
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>123456789101112</code></pre></td>
    <td align="left"><pre><code>&lt;!-- 配置自定义类型转换器   --&gt;    &lt;bean id=&quot;myConversionService&quot; class=&quot;org.springframework.context.support.ConversionServiceFactoryBean&quot;&gt;        &lt;property name=&quot;converters&quot;&gt;            &lt;set&gt;&lt;!--set集合属性--&gt;                &lt;bean class=&quot;com.zephxu.utils.StringToDateConverter&quot;/&gt;                &lt;!--新增--&gt;            &lt;/set&gt;        &lt;/property&gt;    &lt;/bean&gt;&lt;!--    SpringMVC注解支持--&gt;    &lt;mvc:annotation-driven conversion-service=&quot;myConversionService&quot;/&gt;&lt;!--处理器映射器、处理器适配器默认生效，类型转换器需要手动配置使生效--&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    **注意：使用自定义类型转换器后替换了原本的默认，导致1996/12/26方式出错，静待解决！！！**

### [](#六、在控制器中使用原生的ServletAPI对象： "六、在控制器中使用原生的ServletAPI对象：")六、在控制器中使用原生的ServletAPI对象：

只需要在控制器的方法参数定义HttpServletRequest和HttpServletResponse对象。

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testServlet&quot;)    public String testServlet(HttpServletRequest request, HttpServletResponse response){        System.out.println(&quot;获取原生API&quot;);        System.out.println(&quot;request:&quot; + request);        System.out.println(&quot;response:&quot; + response);        System.out.println(&quot;session:&quot; + request.getSession());        System.out.println(&quot;ServletContext:&quot; + request.getServletContext());        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

[](#part4、常用的注解 "part4、常用的注解")part4、常用的注解
-----------------------------------------------------------

### [](#一、RequestParam注解 "一、RequestParam注解")一、RequestParam注解

#### [](#1、作用： "1、作用：")1、作用：

把请求中的指定名称的参数传递给控制器中的形参赋值。

#### [](#2、属性： "2、属性：")2、属性：

a) value（name）：请求参数中的名称

b) required：请求参数中是否必须提供此参数，默认值是true，必须提供

`<a href="annotation/testRequestParameter?name=许xzf">RequestParameter</a>`

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>@Controller@RequestMapping(&quot;/annotation&quot;)public class AnnotationController {    @RequestMapping(&quot;/testRequestParameter&quot;)    public String testRequestParameter(@RequestParam(name = &quot;name&quot;) String username) {        System.out.println(&quot;AnnotationController&quot;);        System.out.println(username);        return &quot;success&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

### [](#二、RequestBody注解（异步，json） "二、RequestBody注解（异步，json）")二、RequestBody注解（异步，json）

#### [](#1、作用：-1 "1、作用：")1、作用：

用于获取请求体的内容（注意：get方法不可以）

**注意：get方法不可以，原因是get方式把内容已经封装到地址栏上。**

#### [](#2、属性：-1 "2、属性：")2、属性：

**required：是否必须有请求体，默认值是true。当取值为 true 时,get
请求方式会报错。如果取值 为 false，get 请求得到是 null。**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>&lt;%--request body注解--%&gt;&lt;%--post--%&gt;&lt;form action=&quot;annotation/testRequestBody&quot; method=&quot;post&quot;&gt;    requestBody 注解 post 请求&lt;br/&gt;    ID：&lt;input type=&quot;text&quot; name=&quot;id&quot;&gt;&lt;br/&gt;    AGE：&lt;input type=&quot;text&quot; name=&quot;age&quot;&gt;&lt;br/&gt;    &lt;input type=&quot;submit&quot; value=&quot;保存&quot;&gt;&lt;/form&gt;&lt;%--get--%&gt;&lt;a href=&quot;annotation/testRequestBody?body=test&quot;&gt;requestBody 注解 get 请求&lt;/a&gt;&quot;</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testRequestBody&quot;)    public String testRequestBody(@RequestBody(required = true) String body) {        System.out.println(&quot;AnnotationController&quot;);        System.out.println(body);        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

-   required = true

-   -   post

    ![post](https://github.com/ZephXu07/IMG/raw/master/TrueRequestBodyTestPost.png)

-   -   get

        ![get](https://github.com/ZephXu07/IMG/raw/master/TrueRequestBodyTestGet.png)

-   required = false

    ![result](https://github.com/ZephXu07/IMG/raw/master/FalseRequestBody.png)

### [](#三、PathVariable注解 "三、PathVariable注解")三、PathVariable注解

#### [](#1、作用：-2 "1、作用：")1、作用：

拥有绑定url中的占位符的。例如：url中有/delete/{id}，{id}就是占位符

![注意](https://github.com/ZephXu07/IMG/raw/master/attention.png)

#### [](#2、属性：-2 "2、属性：")2、属性：

value：指定url中的占位符名称

#### [](#3、Restful风格的URL "3、Restful风格的URL")3、Restful风格的URL

##### [](#a "a)")a)

请求路径一样，可以根据不同的请求方式去执行后台的不同方法

##### [](#b-restful风格的URL优点 "b)    restful风格的URL优点:")b) restful风格的URL优点:

i) 结构清晰

ii) 符合标准

iii) 易于理解

iv) 扩展方便

##### [](#c-restful特性 "c)    restful特性")c) restful特性

![restfulCharacter](https://github.com/ZephXu07/IMG/raw/master/RestfulCharacter.png)

![restfulStyle](https://github.com/ZephXu07/IMG/raw/master/01-restful%E7%BC%96%E7%A8%8B%E9%A3%8E%E6%A0%BC.png)

#### [](#4、实践 "4、实践")4、实践

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12</code></pre></td>
<td align="left"><pre><code>&lt;%--PathVariable--%&gt;    &lt;a href=&quot;annotation/testPathVariable/17&quot;&gt;testPathVariable&lt;/a&gt;&quot;&lt;%--“/”后面直接数字--%&gt;</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testPathVariable/{sid}&quot;)public String testPathVariable(@PathVariable(name = &quot;sid&quot;) String id) {        System.out.println(&quot;AnnotationController&quot;);        System.out.println(id);    return &quot;success&quot;;}</code></pre></td>
</tr>
</tbody>
</table>

![result](https://github.com/ZephXu07/IMG/raw/master/PathVariableResul.png)

### [](#四、基于-HiddentHttpMethodFilter-的示例（了解即可） "四、基于 HiddentHttpMethodFilter 的示例（了解即可）")四、基于 HiddentHttpMethodFilter 的示例（了解即可）

#### [](#1、作用：-3 "1、作用：")1、作用：

由于浏览器 form 表单只支持 GET 与 POST 请求，而DELETE、PUT 等 method
并不支持，Spring3.0
添加了一个过滤器，可以将浏览器请求改为指定的请求方式，发送给我们的控制器方法，使得支持
GET、POST、PUT 与 DELETE 请求。

#### [](#2、使用方法： "2、使用方法：")2、使用方法：

a)：在 web.xml 中配置该过滤器。

b)：请求方式必须使用 post 请求。

c)：按照要求提供\_method 请求参数，该参数的取值就是我们需要的请求方式。

#### [](#3、源码分析： "3、源码分析：")3、源码分析：

![源码](https://github.com/ZephXu07/IMG/raw/master/ResourceCode.png)

jsp 中示例代码：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324</code></pre></td>
<td align="left"><pre><code>&lt;!-- 保存 --&gt; &lt;form action=&quot;springmvc/testRestPOST&quot; method=&quot;post&quot;&gt;     用户名称：&lt;input type=&quot;text&quot; name=&quot;username&quot;&gt;&lt;br/&gt; &lt;!-- &lt;input type=&quot;hidden&quot; name=&quot;_method&quot; value=&quot;POST&quot;&gt; --&gt;     &lt;input type=&quot;submit&quot; value=&quot;保存&quot;&gt;&lt;/form&gt; &lt;hr/&gt; &lt;!-- 更新 --&gt; &lt;form action=&quot;springmvc/testRestPUT/1&quot; method=&quot;post&quot;&gt;     用户名称：&lt;input type=&quot;text&quot; name=&quot;username&quot;&gt;&lt;br/&gt;     &lt;input type=&quot;hidden&quot; name=&quot;_method&quot; value=&quot;PUT&quot;&gt;     &lt;input type=&quot;submit&quot; value=&quot;更新&quot;&gt;&lt;/form&gt;&lt;hr/&gt; &lt;!-- 删除 --&gt; &lt;form action=&quot;springmvc/testRestDELETE/1&quot; method=&quot;post&quot;&gt;     &lt;input type=&quot;hidden&quot; name=&quot;_method&quot; value=&quot;DELETE&quot;&gt;     &lt;input type=&quot;submit&quot; value=&quot;删除&quot;&gt;&lt;/form&gt; &lt;hr/&gt; &lt;!-- 查询一个 --&gt; &lt;form action=&quot;springmvc/testRestGET/1&quot; method=&quot;post&quot;&gt;     &lt;input type=&quot;hidden&quot; name=&quot;_method&quot; value=&quot;GET&quot;&gt;     &lt;input type=&quot;submit&quot; value=&quot;查询&quot;&gt;&lt;/form&gt;</code></pre></td>
</tr>
</tbody>
</table>

控制器中示例代码：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324252627282930313233343536373839</code></pre></td>
<td align="left"><pre><code>/*** post 请求：保存 * @param username * @return */@RequestMapping(value=&quot;/testRestPOST&quot;,method=RequestMethod.POST) public String testRestfulURLPOST(User user){     System.out.println(&quot;rest post&quot;+user);     return &quot;success&quot;;} /*** put 请求：更新 * @param username * @return */@RequestMapping(value=&quot;/testRestPUT/{id}&quot;,method=RequestMethod.PUT) public String testRestfulURLPUT(@PathVariable(&quot;id&quot;)Integer id,User user){     System.out.println(&quot;rest put &quot;+id+&quot;,&quot;+user);     return &quot;success&quot;;} /*** post 请求：删除 * @param username * @return */@RequestMapping(value=&quot;/testRestDELETE/{id}&quot;,method=RequestMethod.DELETE) public String testRestfulURLDELETE(@PathVariable(&quot;id&quot;)Integer id){     System.out.println(&quot;rest delete &quot;+id);}/*** post 请求：查询 * @param username * @return */@RequestMapping(value=&quot;/testRestGET/{id}&quot;,method=RequestMethod.GET) public String testRestfulURLGET(@PathVariable(&quot;id&quot;)Integer id){     System.out.println(&quot;rest get &quot;+id);     return &quot;success&quot;;}</code></pre></td>
</tr>
</tbody>
</table>

运行结果：

![runResult](https://github.com/ZephXu07/IMG/raw/master/RunResult.png)

### [](#五、RequestHeader注解（一般开发中不怎么用） "五、RequestHeader注解（一般开发中不怎么用）")五、RequestHeader注解（一般开发中不怎么用）

#### [](#1、作用：-4 "1、作用：")1、作用：

获取指定请求头的值

#### [](#2、属性：-3 "2、属性：")2、属性：

value：请求头的名称

required：是否必须有此消息头

#### [](#3、实践 "3、实践")3、实践

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12</code></pre></td>
<td align="left"><pre><code>&lt;%--RequestHeader--%&gt;    &lt;a href=&quot;annotation/testRequestHeader&quot;&gt;RequestHeader&lt;/a&gt;&lt;br/&gt;</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testRequestHeader&quot;)   public String testRequestHeader(@RequestHeader(value = &quot;Accept&quot;) String value) {       System.out.println(&quot;AnnotationController&quot;);       System.out.println(value);       return &quot;success&quot;;   }</code></pre></td>
</tr>
</tbody>
</table>

![requestHeaderResult](https://github.com/ZephXu07/IMG/raw/master/RequestHeaderResult.png)

### [](#六、CookieValue注解 "六、CookieValue注解")六、CookieValue注解

#### [](#1、作用：-5 "1、作用：")1、作用：

用于获取指定cookie的名称的值

#### [](#2、属性：-4 "2、属性：")2、属性：

value：cookie的名称

required：是否必须有此 cookie。

#### [](#3、实践-1 "3、实践")3、实践

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12</code></pre></td>
<td align="left"><pre><code>&lt;%--CookieValue--%&gt;    &lt;a href=&quot;annotation/testCookieValue&quot;&gt;CookieValue&lt;/a&gt;&lt;br/&gt;</code></pre></td>
</tr>
</tbody>
</table>

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testCookieValue&quot;)    public String testCookieValue(@CookieValue(&quot;JSESSIONID&quot;) String cookieValue) {        System.out.println(&quot;AnnotationController&quot;);        System.out.println(cookieValue);        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

### [](#七、ModelAttribute注解 "七、ModelAttribute注解")七、ModelAttribute注解

#### [](#1、作用 "1、作用")1、作用

a)
出现在方法上：表示当前方法会在控制器方法执行前线执行，它可以修饰没有返回值的方法，也可以修饰有具体返回值的方法。

b) 出现在参数上：获取指定的数据给参数赋值。

#### [](#2、属性：-5 "2、属性：")2、属性：

value：用于获取数据的 key。key 可以是 POJO 的属性名称，也可以是 map
结构的 key。

#### [](#3、应用场景： "3、应用场景：")3、应用场景：

当提交表单数据不是完整的实体数据时，保证没有提交的字段使用数据库原来的数据。例如：  

我们在编辑一个用户时，用户有一个创建信息字段，该字段的值是不允许被修改的。在提交表单数
据是肯定没有此字段的内容，一旦更新会把该字段内容置为
null，此时就可以使用此注解解决问题。

#### [](#4、实践-1 "4、实践")4、实践

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>&lt;%--ModelAttribute--%&gt;&lt;form action=&quot;annotation/testModelAttribute&quot; method=&quot;post&quot;&gt;          ID：&lt;input type=&quot;text&quot; name=&quot;id&quot;&gt;&lt;br/&gt;        AGE：&lt;input type=&quot;text&quot; name=&quot;age&quot;&gt;&lt;br/&gt;        &lt;input type=&quot;submit&quot; value=&quot;保存&quot;&gt;&lt;/form&gt;</code></pre></td>
</tr>
</tbody>
</table>

**封装User对象，但少了Date属性，更新时会置为null，以下方法解决：**

##### [](#a-方法无返回值： "a)    方法无返回值：")a) 方法无返回值：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617</code></pre></td>
<td align="left"><pre><code>@ModelAttribute    public void show2(Integer id, Map&lt;String, User&gt; userMap) {        System.out.println(&quot;show&quot;);        //模拟数据库查询        User user = new User();        user.setId(id);        user.setAge(20);        user.setDate(new Date());        userMap.put(&quot;a&quot;, user);    }@RequestMapping(&quot;/testModelAttribute&quot;)    public String testModelAttribute(@ModelAttribute(&quot;a&quot;) User user){        System.out.println(&quot;AnnotationController-testModelAttribute&quot;);//        System.out.println(cookieValue);        System.out.println(user);        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

##### [](#b-方法有返回值： "b)    方法有返回值：")b) 方法有返回值：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617</code></pre></td>
<td align="left"><pre><code>@ModelAttribute    public User show(Integer id) {        System.out.println(&quot;show&quot;);        //模拟数据库查询        User user = new User();        user.setId(id);        user.setAge(20);        user.setDate(new Date());        return user;    }@RequestMapping(&quot;/testModelAttribute&quot;)    public String testModelAttribute(User user){        System.out.println(&quot;AnnotationController-testModelAttribute&quot;);//        System.out.println(cookieValue);        System.out.println(user);        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

**从数据库查询后某些数值（已在前端输入的）会被改为前端输入的。**

![注意](https://github.com/ZephXu07/IMG/raw/master/attentionModelAttribute.png)

### [](#八、SessionAttributes（复数） "八、SessionAttributes（复数）")八、SessionAttributes（复数）

#### [](#1、作用：-6 "1、作用：")1、作用：

用于多次执行控制器方法间的参数共享。

#### [](#2、属性 "2、属性")2、属性

value：用于指定存入的属性名称 ；

type：用于指定存入的数据类型。

#### [](#3、实践： "3、实践：")3、实践：

annotation.jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234</code></pre></td>
<td align="left"><pre><code>&lt;%--SessionAttribute--%&gt;&lt;a href=&quot;annotation/testSessionAttributes&quot;&gt;SessionAttribute&lt;/a&gt;&lt;br/&gt;&lt;!--存入--&gt;&lt;a href=&quot;annotation/getSessionAttributes&quot;&gt;getSessionAttribute&lt;/a&gt;&lt;br/&gt;&lt;!--取出--&gt;&lt;a href=&quot;annotation/delSessionAttributes&quot;&gt;delSessionAttribute&lt;/a&gt;&lt;br/&gt;&lt;!--删除--&gt;</code></pre></td>
</tr>
</tbody>
</table>

success.jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123</code></pre></td>
<td align="left"><pre><code>${requestScope.get(&quot;phy&quot;)}&lt;br/&gt;${phy}&lt;br/&gt;${sessionScope.get(&quot;phy&quot;)}&lt;br/&gt;</code></pre></td>
</tr>
</tbody>
</table>

-   `@SessionAttributes(value = {"phy"})`在类上面标注，可多个，{}中是key

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testSessionAttributes&quot;)    public String testSessionAttributes(Model model){        System.out.println(&quot;testSessionAttribute&quot;);        //Model类可降低耦合，底层存储到Request域对象中        model.addAttribute(&quot;phy&quot;, &quot;xzf&quot;);        return &quot;success&quot;;    }    @RequestMapping(&quot;/getSessionAttributes&quot;)    public String getSessionAttributes(ModelMap modelMap){        System.out.println(&quot;getSessionAttribute&quot;);        String info = (String) modelMap.getAttribute(&quot;phy&quot;);        //实现了多次执行控制器方法间的参数共享。        System.out.println(info);        return &quot;success&quot;;    }    @RequestMapping(&quot;/delSessionAttributes&quot;)    public String delSessionAttributes(SessionStatus status){        System.out.println(&quot;delSessionAttribute&quot;);        status.setComplete();        //删除session        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

![结果](https://github.com/ZephXu07/IMG/raw/master/SessionAttributeResult.png)

[](#part5、响应数据和结果视图 "part5、响应数据和结果视图")part5、响应数据和结果视图
-----------------------------------------------------------------------------------

-   响应的方式：

    ![ResponseWays](https://github.com/ZephXu07/IMG/raw/master/ResponseWays.png)

### [](#一、返回值分类 "一、返回值分类")一、返回值分类

#### [](#1、返回字符串 "1、返回字符串")1、返回字符串

Controller方法返回字符串可以指定逻辑视图的名称，根据视图解析器为物理视图的地址。

视图解析器配置：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456</code></pre></td>
<td align="left"><pre><code>&lt;!--视图解析器--&gt;    &lt;bean id=&quot;internalResourceViewResolver&quot; class=&quot;org.springframework.web.servlet.view.InternalResourceViewResolver&quot;&gt;        &lt;property name=&quot;prefix&quot; value=&quot;/WEB-INF/pages/&quot;/&gt;        &lt;property name=&quot;suffix&quot; value=&quot;.jsp&quot;/&gt;        &lt;!--前后缀连接成页面的文件--&gt;    &lt;/bean&gt;</code></pre></td>
</tr>
</tbody>
</table>

![pages](https://github.com/ZephXu07/IMG/raw/master/Pages.png)

UserCtroller：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516</code></pre></td>
<td align="left"><pre><code>@Controller@RequestMapping(&quot;/user&quot;)public class UserController {    @RequestMapping(&quot;/testString&quot;)    public String testString(Model model) {        System.out.println(&quot;testString&quot;);        //模拟从数据库查找        User user = new User();        user.setUsername(&quot;xzf&quot;);        user.setPassword(&quot;phy&quot;);        user.setAge(20);        //Model对象        model.addAttribute(&quot;user&quot;, user);        return &quot;success&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

success.jsp：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; isELIgnored=&quot;false&quot; %&gt;&lt;html&gt;    &lt;head&gt;            &lt;title&gt;Success&lt;/title&gt;    &lt;/head&gt;    &lt;body&gt;            &lt;h1&gt;Success&lt;/h1&gt;            ${user.toString()}    &lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

![successResult](https://github.com/ZephXu07/IMG/raw/master/SuccessResult.png)

#### [](#2、返回值是void "2、返回值是void")2、返回值是void

1、如果控制器的方法返回值编写成void，执行程序报404的异常，默认查找JSP页面没有找到，原因是默认会跳转到`@RequestMapping("/testVoid")`中的testVoid.jsp的页面。

2、可以使用请求转发或者重定向跳转到指定的页面，或者直接响应

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testVoid&quot;)    public void testVoid(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {        System.out.println(&quot;testVoid&quot;);        /*请求转发，不需要编写项目的名称，但是仍需要写部分路径，原因是不返回字符串，        视图解析器不会工作，且转发后再执行后续代码，用return 停止        *///        request.getRequestDispatcher(&quot;/WEB-INF/pages/success.jsp&quot;).forward(request, response);//        return;        /*            重定向，两次转发，页面需要重新详细写，            request.getContextPath()            拿到springmvc_day_02_01_response_war_exploded路径，此地方只有Index.jsp         *///        response.sendRedirect(request.getContextPath() + &quot;/index.jsp&quot;);        /*直接响应：浏览器直接发请求，控制器通过输出流直接响应会浏览器        设置解决中文乱码*/        response.setCharacterEncoding(&quot;UTF-8&quot;);        response.setContentType(&quot;text/html;charset=UTF-8&quot;);        //response.setContentType(&quot;application/json;charset=utf-8&quot;);        response.getWriter().println(&quot;直接响应&quot;);    }</code></pre></td>
</tr>
</tbody>
</table>

#### [](#3-返回值是ModelAndView对象（与返回字符串方式类似） "3. 返回值是ModelAndView对象（与返回字符串方式类似）")3. 返回值是ModelAndView对象（与返回字符串方式类似）

a)、ModelAndView对象是Spring提供的一个对象，可以用来调整具体的JSP视图

b)、实践

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testModelAndView&quot;)    public ModelAndView testModelAndView() {        System.out.println(&quot;testModelAndView&quot;);        //创建ModelAndView对象        ModelAndView mv = new ModelAndView();        //模拟从数据库查找        User user = new User();        user.setUsername(&quot;phy&quot;);        user.setPassword(&quot;xzf&quot;);        user.setAge(22);        //把user对象存储到mv对象中，也会把user对象存入request域对象        mv.addObject(&quot;user&quot;, user);        //跳转到哪个页面，使用视图解析器        mv.setViewName(&quot;success&quot;);        return mv;    }</code></pre></td>
</tr>
</tbody>
</table>

c)、**注意： 我们在页面上上获取使用的是 requestScope.username
取的，所以返回 ModelAndView 类型时，浏 览器跳转只能是请求转发。**

### [](#二、SpringMVC框架提供的转发和重定向 "二、SpringMVC框架提供的转发和重定向")二、SpringMVC框架提供的转发和重定向

#### [](#1、forward请求转发 "1、forward请求转发")1、forward请求转发

controller方法返回String类型，想进行请求转发也可以编写成

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234</code></pre></td>
<td align="left"><pre><code>//请求转发：不使用视图解析器    return &quot;forward:/WEB-INF/pages/success.jsp&quot;;//相当于“request.getRequestDispatcher(&quot;url&quot;).forward(request,response)”。// 使用请求 转发，既可以转发到 jsp，也可以转发到其他的控制器方法。</code></pre></td>
</tr>
</tbody>
</table>

#### [](#2、redirect重定向 "2、redirect重定向")2、redirect重定向

controller方法返回String类型，想进行重定向也可以编写成

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234</code></pre></td>
<td align="left"><pre><code>//重定向：不需要加项目名        return &quot;redirect:/index.jsp&quot;;//相当于“response.sendRedirect(url)”。需要注意的是，// 如果是重定向到 jsp 页面，则 jsp 页面不 能写在 WEB-INF 目录中，否则无法找到。</code></pre></td>
</tr>
</tbody>
</table>

### [](#三、ResponseBody响应json数据 "三、ResponseBody响应json数据")三、ResponseBody响应json数据

#### [](#1、DispatcherServlet "1、DispatcherServlet")1、DispatcherServlet

DispatcherServlet会拦截到所有的资源，导致一个问题就是静态资源（img、css、js）也会被拦截到，从而
不能被使用。解决问题就是需要配置静态资源不进行拦截，在springmvc.xml配置文件添加如下配置

a) location元素表示webapp目录下的包下的所有文件

b) mapping元素表示以/static开头的所有请求路径，如/static/a
或者/static/a/b

添加配置SpringMVC.xml配置：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234</code></pre></td>
<td align="left"><pre><code>&lt;!-- 设置静态资源不过滤 --&gt; &lt;mvc:resources location=&quot;/css/&quot; mapping=&quot;/css/**&quot;/&gt; &lt;!-- 样式 --&gt; &lt;mvc:resources location=&quot;/images/&quot; mapping=&quot;/images/**&quot;/&gt; &lt;!-- 图片 --&gt; &lt;mvc:resources location=&quot;/js/&quot; mapping=&quot;/js/**&quot;/&gt; &lt;!-- javascript --&gt;</code></pre></td>
</tr>
</tbody>
</table>

**配置一字不落的不能改变，location少了后面一个/都不能用了！！！**

#### [](#2、使用-RequestBody获取请求体数据（点击查看作用） "2、使用@RequestBody获取请求体数据（点击查看作用）")2、使用@RequestBody获取请求体数据[（点击查看作用）](#RequestBody)

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617181920212223</code></pre></td>
<td align="left"><pre><code> &lt;%--  User: ZephXU  Date: 2019/10/10  Time: 19:12--%&gt;&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;Response&lt;/title&gt;    &lt;script src=&quot;js/jquery.min.js&quot;&gt;&lt;/script&gt;    &lt;script&gt;        //页面加载，绑定单击事件        $(function () {            $(&quot;#btn&quot;).click(function () {                alert(&quot;hello button&quot;)            })        })    &lt;/script&gt;&lt;/head&gt;&lt;body&gt;    &lt;button id=&quot;btn&quot;&gt;发送ajax请求&lt;/button&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

UserController.java

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567</code></pre></td>
<td align="left"><pre><code>//模拟异步请求响应    @RequestMapping(&quot;/testAjax&quot;)    public String testAjax(@RequestBody String body) {        System.out.println(&quot;testAjax&quot;);        System.out.println(body);        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

**无任何响应！[原因](#dispatcherServlet)**

#### [](#3、使用-RequestBody注解把json的字符串转换成JavaBean的对象 "3、使用@RequestBody注解把json的字符串转换成JavaBean的对象")3、使用@RequestBody注解把json的字符串转换成JavaBean的对象

#### [](#4、使用-ResponseBody注解把JavaBean对象转换成json字符串，直接响应 "4、使用@ResponseBody注解把JavaBean对象转换成json字符串，直接响应")4、使用@ResponseBody注解把JavaBean对象转换成json字符串，直接响应

a)
作用：该注解用于将Controller的方法返回的对象，通过HttpMessageConverter接口转换为指定格式的
数据如：json,xml 等，通过 Response 响应给客户端

b) **Springmvc 默认用 MappingJacksonHttpMessageConverter 对 json
数据进行转换，需要加入jackson 的包。**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718</code></pre></td>
<td align="left"><pre><code>&lt;!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind --&gt;    &lt;dependency&gt;      &lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;      &lt;artifactId&gt;jackson-databind&lt;/artifactId&gt;      &lt;version&gt;${jackson.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations --&gt;    &lt;dependency&gt;      &lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;      &lt;artifactId&gt;jackson-annotations&lt;/artifactId&gt;      &lt;version&gt;${jackson.version}&lt;/version&gt;    &lt;/dependency&gt;    &lt;!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core --&gt;    &lt;dependency&gt;      &lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;      &lt;artifactId&gt;jackson-core&lt;/artifactId&gt;      &lt;version&gt;${jackson.version}&lt;/version&gt;    &lt;/dependency&gt;</code></pre></td>
</tr>
</tbody>
</table>

`${jackson.version}`前文已写。

c) response.jsp：**按钮方法改变！！！**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819202122</code></pre></td>
<td align="left"><pre><code>&lt;script&gt;        //页面加载，绑定单击事件        $(function () {            $(&quot;#btn&quot;).click(function () {                alert(&quot;看控制台&quot;);                //编写json格式，设置属性和值                $.ajax({                    url:&quot;user/testAjax&quot;,                    contentType:&quot;application/json;charset=UTF-8&quot;,                    data:&#39;{&quot;username&quot;:&quot;phy&quot;,&quot;password&quot;:&quot;phy&quot;,&quot;age&quot;:22}&#39;,                    dataType:&quot;json&quot;,                    type:&quot;post&quot;,                    success:function (data) {                        //data服务器端响应的json的数据，进行解析                        alert(data + &quot;\n&quot; + data.username + &quot;\n&quot;                            + data.password + &quot;\n&quot;                            + data.age);                    }                })            });        });    &lt;/script&gt;</code></pre></td>
</tr>
</tbody>
</table>

d) UserController.java新的控制方法：

-   把json的字符串转换成JavaBean的对象
-   方法需要返回JavaBean的对象

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213</code></pre></td>
<td align="left"><pre><code>//模拟异步请求响应    @RequestMapping(&quot;/testAjax&quot;)    public @ResponseBody User testAjax(@RequestBody User user) {        System.out.println(&quot;testAjax&quot;);        //客户端发送Ajax请求，传的是json字符串，后端把json字符串封装到user对象中        System.out.println(user);        //做响应，模拟查询数据库，与客户端传来数据少许不同        user.setUsername(&quot;xzf&quot;);        user.setPassword(&quot;xzf&quot;);        user.setAge(19);        //做响应，返回新的数据        return user;    }</code></pre></td>
</tr>
</tbody>
</table>

e) 结果：

![result1](https://github.com/ZephXu07/IMG/raw/master/JsonResult1.png)

![result2](https://github.com/ZephXu07/IMG/raw/master/JsonResult2.png)

![result3](https://github.com/ZephXu07/IMG/raw/master/JsonResult3.png)

[](#part6、SpringMVC实现文件上传 "part6、SpringMVC实现文件上传")part6、SpringMVC实现文件上传
--------------------------------------------------------------------------------------------

### [](#1、传统文件上传的回顾 "1、传统文件上传的回顾")1、传统文件上传的回顾

#### [](#a-、必要前提 "a)、必要前提")a)、必要前提

i)、form 表单的 enctype 取值必须是：**multipart/form-data**

(默认值是:**application/x-www-form-urlencoded**，即以键值对形式：`username=xzf&passwprd=10709991`)  
 enctype:是表单请求正文的类型  
 ii)、method 属性取值必须是 Post ，Get会写在地址栏，大小有限

iii)、提供一个文件选择域\`\`\`

#### [](#b-、原理分析 "b)、原理分析")b)、原理分析

当 form 表单的 enctype 取值不是默认值后，request.getParameter()将失效。
enctype=”application/x-www-form-urlencoded”时，form 表单的正文内容是：
key=value&key=value&key=value  
当 form 表单的 enctype 取值为 Mutilpart/form-data
时，请求正文内容就变成：每一部分都是 MIME 类型描述的正文

—————————–7de1a433602ac 分界符  
 Content-Disposition: form-data; name=”userName” 协议头

aaa  
 —————————–7de1a433602ac 协议的正文

Content-Disposition: form-data;  
filename=”C:\\Users\\zhy\\Desktop\\fileupload\_demofile\\b.txt”

Content-Type: text/plain 协议的类型（MIME 类型）  
 bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb

—————————–7de1a433602ac–

#### [](#c-、借助第三方组件实现文件上传 "c)、借助第三方组件实现文件上传")c)、借助第三方组件实现文件上传

使用 Commons-fileupload 组件实现文件上传，需要导入该组件相应的支撑 jar
包：Commons-fileupload 和commons-io。commons-io
不属于文件上传组件的开发jar 文件，但Commons-fileupload 组件从1.1
版本开始，它 工作时需要 commons-io 包的支持。

#### [](#d-、代码： "d)、代码：")d)、代码：

文件上传的JSP页面：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718</code></pre></td>
<td align="left"><pre><code>&lt;%--  User: ZephXU  Date: 2019/10/12  Time: 19:00--%&gt;&lt;%@ page contentType=&quot;text/html;charset=UTF-8&quot; language=&quot;java&quot; %&gt;&lt;html&gt;&lt;head&gt;    &lt;title&gt;文件上传&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&lt;h1&gt;文件上传&lt;/h1&gt;&lt;form action=&quot;user/fileUpload0&quot; method=&quot;post&quot; enctype=&quot;multipart/form-data&quot;&gt;    选择上传文件：&lt;input type=&quot;file&quot; name=&quot;upload&quot;/&gt;&lt;br/&gt;    &lt;input type=&quot;submit&quot; value=&quot;上传&quot;&gt;&lt;/form&gt;&lt;/body&gt;&lt;/html&gt;</code></pre></td>
</tr>
</tbody>
</table>

文件上传的Controller控制器：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819202122232425262728293031323334353637383940414243</code></pre></td>
<td align="left"><pre><code>@Controller@RequestMapping(&quot;/user&quot;)public class UserController {    @RequestMapping(&quot;/fileUpload0&quot;)    public String fileUpload0(HttpServletRequest request) throws Exception {        System.out.println(&quot;fileUpload0&quot;);        //使用fileupload组件完成文件上传        //上传的位置        String path = request.getSession().getServletContext().getRealPath(&quot;/uploads/&quot;);        //判断该路径是否存在        File file = new File(path);        if (!file.exists()) {            //创建该文件夹            file.mkdirs();        }        //解析request对象，获取上传文件项        DiskFileItemFactory factory = new DiskFileItemFactory();        ServletFileUpload upload = new ServletFileUpload(factory);        //解析request        List&lt;FileItem&gt; items = upload.parseRequest(request);        //遍历        for (FileItem item: items) {            if (!item.isFormField()) {                //不是普通表单，文件                //获取文件名称                String fileName  = item.getName();                //fileName带盘符，在创建新文件因与path的所在盘可能                // 不同造成bug：文件名、目录名或卷标语法不正确。                String fileTrueName = fileName.substring(fileName.lastIndexOf(&quot;\\&quot;)+1);                //获得单纯文件名                //把文件名称设置为唯一值，UUID                String uuid = UUID.randomUUID().toString().replace(&quot;-&quot;, &quot;&quot;);                fileTrueName = uuid + &quot;_&quot; + fileTrueName;                //完成文件上传                item.write(new File(path, fileTrueName));                //删除临时文件，上传文件大小大于10KB产生临时文件，小于10KB则在内存中生成缓存文件                item.delete();            }        }        return &quot;success&quot;;    }}</code></pre></td>
</tr>
</tbody>
</table>

**BUG：文件名、目录名或卷标语法不正确。**

**原因：fileName带盘符，在创建新文件因与path的所在盘可能不同造成bug。**

[解决方案](https://www.iteye.com/blog/rogerfederer-1039666)

### [](#2、SpringMVC传统方式文件上传 "2、SpringMVC传统方式文件上传")2、SpringMVC传统方式文件上传

a)、SpringMVC框架提供了MultipartFile对象，该对象表示上传的文件，**要求变量名称必须和表单file标签的
name属性名称相同。**

b)、原理图：**图中注意事项**

![原理图](https://github.com/ZephXu07/IMG/raw/master/SpringMVCUpload.png)

c)、配置文件解析器对象

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345</code></pre></td>
<td align="left"><pre><code>&lt;!--配置文件解析器对象，id必须是multipartResolver--&gt;    &lt;bean id=&quot;multipartResolver&quot; class=&quot;org.springframework.web.multipart.commons.CommonsMultipartResolver&quot;&gt;        &lt;property name=&quot;maxUploadSize&quot; value=&quot;10485760&quot;/&gt;           &lt;!--文件上传最大大小单位字节：10*1024*1024--&gt;    &lt;/bean&gt;</code></pre></td>
</tr>
</tbody>
</table>

d)、Controller方法（只是改变些许）：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819202122</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/fileUpload1&quot;)    public String fileUpload1(HttpServletRequest request, MultipartFile upload) throws Exception {        //注意upload需要和表单的文件上传的name一样        System.out.println(&quot;fileUpload1&quot;);        //使用fileupload组件完成文件上传        //上传的位置        String path = request.getSession().getServletContext().getRealPath(&quot;/uploads/&quot;);        //判断该路径是否存在        File file = new File(path);        if (!file.exists()) {            //创建该文件夹            file.mkdirs();        }        //获取文件名称        String fileName  = upload.getOriginalFilename();        //把文件名称设置为唯一值，UUID        String uuid = UUID.randomUUID().toString().replace(&quot;-&quot;, &quot;&quot;);        fileName = uuid + &quot;_&quot; + fileName;        //完成文件上传        upload.transferTo(new File(path, fileName));        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

### [](#3、SpringMVC跨服务器方式文件上传 "3、SpringMVC跨服务器方式文件上传")3、SpringMVC跨服务器方式文件上传

#### [](#1、搭建图片服务器： "1、搭建图片服务器：")1、搭建图片服务器：

a)、分服务器的目的：

在实际开发中，我们会有很多处理不同功能的服务器。例如：

应用服务器：负责部署我们的应用

数据库服务器：运行我们的数据库  
 缓存和消息服务器：负责处理大并发访问的缓存和消息

文件服务器：负责存储用户上传文件的服务器。

(注意：此处说的不是服务器集群）

分服务器处理的目的是让服务器各司其职，从而提高我们项目的运行效率。

![FileUploadsAcrossServers](https://github.com/ZephXu07/IMG/raw/master/FileUploadsAcrossServers.png)

![Purpose of
sub-server](https://github.com/ZephXu07/IMG/raw/master/PurposeOfSub-server.png)

b)、再创建 tomcat 服务器，并创建一个用于存放图片的 web工程：

如图：

![FileServer](https://github.com/ZephXu07/IMG/raw/master/FileServerStructure.png)

在**apache-tomcat-8.5.40\\conf目录下的web.xml加入内容：**

![Configuration](https://github.com/ZephXu07/IMG/raw/master/AddTheConfiguration.png)

**bug：com.sun.jersey.api.client.UniformInterfaceException: PUT
[http://localhost:9090/fileuploadserver\_war\_exploded/uploads/04694da7a10a4a98b68690ad6426a120\_ShowUserAgent.html](http://localhost:9090/fileuploadserver_war_exploded/uploads/04694da7a10a4a98b68690ad6426a120_ShowUserAgent.html)
returned a response status of 409 Conflict**

**原因：项目的target目录下没有存储上传文件的目录，如[上图](#uploads)**

[参考博客](https://blog.csdn.net/Java_3y/article/details/84908247)

#### [](#2、实现SpringMVC跨服务器方式文件上传 "2、实现SpringMVC跨服务器方式文件上传")2、实现SpringMVC跨服务器方式文件上传

a)、导入开发需要的jar包

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>&lt;dependency&gt;     &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;     &lt;artifactId&gt;jersey-core&lt;/artifactId&gt;        &lt;version&gt;1.18.1&lt;/version&gt;&lt;/dependency&gt;&lt;dependency&gt;    &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;     &lt;artifactId&gt;jersey-client&lt;/artifactId&gt;     &lt;version&gt;1.18.1&lt;/version&gt;&lt;/dependency&gt;</code></pre></td>
</tr>
</tbody>
</table>

b)、编写文件上传的JSP页面

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345</code></pre></td>
<td align="left"><pre><code>&lt;h1&gt;SpringMVC跨服务器文件上传&lt;/h1&gt;&lt;form action=&quot;user/fileUpload2&quot; method=&quot;post&quot; enctype=&quot;multipart/form-data&quot;&gt;    选择上传文件：&lt;input type=&quot;file&quot; name=&quot;upload&quot;/&gt;&lt;br/&gt;    &lt;input type=&quot;submit&quot; value=&quot;上传&quot;&gt;&lt;/form&gt;</code></pre></td>
</tr>
</tbody>
</table>

c)、编写控制器

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910111213141516171819</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/fileUpload2&quot;)    public String fileUpload2(MultipartFile upload) throws Exception {        System.out.println(&quot;fileUpload2&quot;);        //定义上传文件服务器路径        String path = &quot;http://localhost:9090/fileuploadserver_war_exploded/uploads/&quot;;        //获取文件名称        String fileName  = upload.getOriginalFilename();        //把文件名称设置为唯一值，UUID        String uuid = UUID.randomUUID().toString().replace(&quot;-&quot;, &quot;&quot;);        fileName = uuid + &quot;_&quot; + fileName;        //完成文件跨服务器上传            //创建客户端对象        Client client = Client.create();            //和图片服务器进行连接        WebResource webResource = client.resource(path + fileName);            //上传        webResource.put(upload.getBytes());        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

[](#part7、SpringMVC的异常处理 "part7、SpringMVC的异常处理")part7、SpringMVC的异常处理
--------------------------------------------------------------------------------------

### [](#1、异常处理思路 "1、异常处理思路")1、异常处理思路

系统中异常包括两类：预期异常和运行时异常
RuntimeException，前者通过捕获异常从而获取异常信息，
后者主要通过规范代码开发、测试通过手段减少运行时异常的发生。

系统的 dao、service、controller 出现都通过 throws Exception
向上抛出，最后由 springmvc 前端
控制器交由异常处理器进行异常处理，如下图：

![SpringMVCExceptionHandler](https://github.com/ZephXu07/IMG/raw/master/SpringMVCExceptionHandler.png)

### [](#2、SpringMVC的异常处理 "2、SpringMVC的异常处理")2、SpringMVC的异常处理

##### [](#a-、不进行处理： "a)、不进行处理：")a)、不进行处理：

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567</code></pre></td>
<td align="left"><pre><code>@RequestMapping(&quot;/testException&quot;)    public String testException() throws Exception{        System.out.println(&quot;testException&quot;);        //模拟异常        int exception = 1 / 0;        return &quot;success&quot;;    }</code></pre></td>
</tr>
</tbody>
</table>

![Don't handle
exception](https://github.com/ZephXu07/IMG/raw/master/DontHandleException.png)

##### [](#b-、异常处理 "b)、异常处理")b)、异常处理

###### [](#i-、自定义异常类：继承Exception "i)、自定义异常类：继承Exception")i)、自定义异常类：继承Exception

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617181920</code></pre></td>
<td align="left"><pre><code>public class SystemException extends Exception {        public SystemException(String message) {        this.message = message;    }    /**     * 存储提示信息     */    private String message;    @Override    public String getMessage() {        return message;    }    public void setMessage(String message) {        this.message = message;    }}</code></pre></td>
</tr>
</tbody>
</table>

###### [](#ii-、自定义异常处理器 "ii)、自定义异常处理器")ii)、自定义异常处理器

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>123456789101112131415161718192021222324252627</code></pre></td>
<td align="left"><pre><code>public class SystemExceptionResolver implements HandlerExceptionResolver {    /**     * Controller抛出异常，前端控制器调用异常处理器，此方法将会执行     * 此方法作用为处理异常业务逻辑     * @param httpServletRequest 请求     * @param httpServletResponse 响应     * @param o 处理器对象     * @param e controller抛出的异常对象     * @return ModelAndView对象     */    @Override    public ModelAndView resolveException(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) {        SystemException se = null;        if (e instanceof SystemException) {            //如果抛出的是系统自定义异常则直接转换            se = (SystemException) e;        } else {            //如果抛出的不是系统自定义异常则重新构造一个系统错误异常。            se = new SystemException(&quot;系统正在维护……&quot;);        }        //创建ModelAndView对象        ModelAndView mv = new ModelAndView();        mv.addObject(&quot;errorMsg&quot;, se.getMessage());        mv.setViewName(&quot;error&quot;);        return mv;    }}</code></pre></td>
</tr>
</tbody>
</table>

###### [](#iii-、配置异常处理器 "iii)、配置异常处理器")iii)、配置异常处理器

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12</code></pre></td>
<td align="left"><pre><code>&lt;!--配置异常处理器--&gt;&lt;bean id=&quot;systemExceptionResolver&quot; class=&quot;com.zephxu.exception.SystemExceptionResolver&quot;/&gt;</code></pre></td>
</tr>
</tbody>
</table>

###### [](#iv-、结果 "iv)、结果")iv)、结果

![HandleExceptionResult](https://github.com/ZephXu07/IMG/raw/master/HandleExceptionResult.png)

[](#part8、SpringMVC框架中的拦截器 "part8、SpringMVC框架中的拦截器")part8、SpringMVC框架中的拦截器
--------------------------------------------------------------------------------------------------

### [](#1、拦截器的概述 "1、拦截器的概述")1、拦截器的概述

a)、SpringMVC框架中的拦截器用于**对处理器进行预处理和后处理**的技术。

b)、可以定义拦截器链，拦截器链就是将拦截器按着一定的顺序结成一条链，在访问被拦截的方法时，拦截器链中的拦截器会按着定义的顺序执行。

c)、拦截器和过滤器的功能比较类似，有区别

 i)、过滤器是Servlet规范的一部分，任何框架都可以使用过滤器技术。

 ii)、拦截器是SpringMVC框架独有的。

 iii)、过滤器配置了/\*，可以拦截任何资源。


iv)、**拦截器只会对控制器中的方法进行拦截，如果访问的是jsp，html，css，image
或者 js是不会进行拦截的。**

 v)、拦截器也是AOP思想的一种实现方式 。

 vi)、想要自定义拦截器，需要实现HandlerInterceptor接口。

![Interceptor](https://github.com/ZephXu07/IMG/raw/master/Interceptor.png)

### [](#2、自定义拦截器步骤 "2、自定义拦截器步骤")2、自定义拦截器步骤

a)、创建类，实现HandlerInterceptor接口，重写需要的方法

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617</code></pre></td>
<td align="left"><pre><code>public class MyInterceptor implements HandlerInterceptor {    /**     * 预处理，controller方法执行前     * @param request     * @param response 不放行时使用转发或者重定向可跳转某页面或怎样处理     * @param handler     * @return true：放行，执行下一个拦截器，没有则执行controller     * false：不放行     * @throws Exception     */    @Override    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {        System.out.println(&quot;MyInterceptor执行了&quot;);        return true;    }}</code></pre></td>
</tr>
</tbody>
</table>

b)、在springmvc.xml中配置拦截器类

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>12345678910</code></pre></td>
<td align="left"><pre><code>&lt;!--配置拦截器--&gt;    &lt;mvc:interceptors&gt;        &lt;mvc:interceptor&gt;            &lt;!--要拦截的具体方法，除此外不拦截--&gt;            &lt;mvc:mapping path=&quot;/user/*&quot;/&gt;&lt;!--“/**”拦截全部，其他类似--&gt;&lt;!--            &lt;mvc:exclude-mapping path=&quot;&quot;/&gt;&amp;lt;!&amp;ndash;不要拦截的具体方法，除此外拦截&amp;ndash;&amp;gt;--&gt;            &lt;!--配置拦截器对象--&gt;            &lt;bean class=&quot;com.zephxu.interceptor.MyInterceptor&quot;/&gt;        &lt;/mvc:interceptor&gt;    &lt;/mvc:interceptors&gt;</code></pre></td>
</tr>
</tbody>
</table>

c)、结果：

![Interceptor
Result](https://github.com/ZephXu07/IMG/raw/master/InterceptorResult.png)

### [](#3、HandlerInterceptor接口中的方法 "3、HandlerInterceptor接口中的方法")3、HandlerInterceptor接口中的方法

a)、preHandle方法是controller方法执行前拦截的方法

 i) 可以使用request或者response跳转到指定的页面 （**若return
true，controller方法跳转的页面将不会显示**）

`request.getRequestDispatcher("/WEB-INF/pages/error.jsp").forward(request, response);`

 ii) return
true放行，执行下一个拦截器，如果没有拦截器，执行controller中的方法。

 iii) return false不放行，不会执行controller中的方法。

b)、postHandle是controller方法执行后执行的方法，在JSP视图执行前。

 i) 可以使用request或者response跳转到指定的页面

 ii)
如果指定了跳转的页面，那么controller方法跳转的页面将不会显示。（jsp代表的java类还是会执行）

c) afterCompletion方法是在JSP执行后执行

-   request或者response不能再跳转页面了

### [](#4、配置多个拦截器 "4、配置多个拦截器")4、配置多个拦截器

-   执行顺序

![InterceptorExecutionProcess](https://github.com/ZephXu07/IMG/raw/master/InterceptorExecutionProcess.png)

-   **多个拦截器是按照配置的顺序决定的。**

<table>
<col width="50%" />
<col width="50%" />
<tbody>
<tr class="odd">
<td align="left"><pre><code>1234567891011121314151617</code></pre></td>
<td align="left"><pre><code>&lt;!--配置拦截器--&gt;    &lt;mvc:interceptors&gt;        &lt;mvc:interceptor&gt;            &lt;!--要拦截的具体方法，除此外不拦截--&gt;            &lt;mvc:mapping path=&quot;/user/*&quot;/&gt;&lt;!--“/**”拦截全部，其他类似--&gt;&lt;!--            &lt;mvc:exclude-mapping path=&quot;&quot;/&gt;&amp;lt;!&amp;ndash;不要拦截的具体方法，除此外拦截&amp;ndash;&amp;gt;--&gt;            &lt;!--配置拦截器对象--&gt;            &lt;bean class=&quot;com.zephxu.interceptor.MyInterceptor&quot;/&gt;        &lt;/mvc:interceptor&gt;        &lt;mvc:interceptor&gt;            &lt;!--要拦截的具体方法，除此外不拦截--&gt;            &lt;mvc:mapping path=&quot;/**&quot;/&gt;&lt;!--“/**”拦截全部，其他类似--&gt;            &lt;!--            &lt;mvc:exclude-mapping path=&quot;&quot;/&gt;&amp;lt;!&amp;ndash;不要拦截的具体方法，除此外拦截&amp;ndash;&amp;gt;--&gt;            &lt;!--配置拦截器对象--&gt;            &lt;bean class=&quot;com.zephxu.interceptor.MyInterceptor2&quot;/&gt;        &lt;/mvc:interceptor&gt;    &lt;/mvc:interceptors&gt;</code></pre></td>
</tr>
</tbody>
</table>

-   结果：

    ![TwoInterceptors](https://github.com/ZephXu07/IMG/raw/master/TwoInterceptors.png)

### [](#part9、SpringMVC暂告一段落……未完待续…… "part9、SpringMVC暂告一段落……未完待续……")part9、SpringMVC暂告一段落……未完待续……

[](javascript:;)

赏

**谢谢你请我吃糖果**

![](/assets/img/alipay.jpg) 支付宝

![](/assets/img/wechatpay.png) 微信

**

-   [笔记](javascript:void(0))
-   [SpringMVC](javascript:void(0))
-   [框架](javascript:void(0))
-   [Java](javascript:void(0))

[**](javascript:;)

[**](javascript:;) [**](javascript:;) [**](javascript:;)
[**](javascript:;) [**](javascript:;) [**](javascript:;)
[**](javascript:;) [**](javascript:;)

[**](javascript:;)

扫一扫，分享到微信

![微信分享二维码](//pan.baidu.com/share/qrcode?url=http://yoursite.com/2019/10/05/SpringMVC-Learning-Notes/)

[**](/2019/10/08/百感乱记/)

百感乱记

[](/2019/10/02/动态代理笔记/)

动态代理笔记

**

[**](javascript:void(0))

**

**

1.  [1. SpringMVC 个人学习笔记](#SpringMVC-个人学习笔记)
    1.  [1.1. part1、三层架构和MVC](#part1、三层架构和MVC)
        1.  [1.1.1. 一、三层架构](#一、三层架构)
        2.  [1.1.2. 二、MVC模型](#二、MVC模型)

    2.  [1.2. part2、SpringMVC的入门案例](#part2、SpringMVC的入门案例)
        1.  [1.2.1. 一、SpringMVC的概述](#一、SpringMVC的概述)
            1.  [1.2.1.1. 1、SpringMVC的概述](#1、SpringMVC的概述)
            2.  [1.2.1.2.
                2、SpringMVC在三层架构中的位置：表现层框架](#2、SpringMVC在三层架构中的位置：表现层框架)
            3.  [1.2.1.3. 3、SpringMVC的优势](#3、SpringMVC的优势)
            4.  [1.2.1.4.
                4、SpringMVC和Stru2的对比](#4、SpringMVC和Stru2的对比)
                1.  [1.2.1.4.1. 共同点：](#共同点：)
                2.  [1.2.1.4.2. 区别：](#区别：)

        2.  [1.2.2. 二、SpringMVC的入门程序](#二、SpringMVC的入门程序)
            1.  [1.2.2.1.
                1、创建Web工程，引入开发的jar包](#1、创建Web工程，引入开发的jar包)
                1.  [1.2.2.1.1. 具体坐标如下](#具体坐标如下)

            2.  [1.2.2.2.
                2、配置核心的控制器（配置DispatcherServlet）](#2、配置核心的控制器（配置DispatcherServlet）)
                1.  [1.2.2.2.1.
                    在web.xml配置文件中核心控制器DispatcherServlet](#在web-xml配置文件中核心控制器DispatcherServlet)

            3.  [1.2.2.3.
                3、编写springmvc.xml的配置文件](#3、编写springmvc-xml的配置文件)
            4.  [1.2.2.4. 4.
                编写index.jsp和HelloController控制器](#4-编写index-jsp和HelloController控制器)
                1.  [1.2.2.4.1. a) index.jsp：](#a-index-jsp：)
                2.  [1.2.2.4.2. b) HelloController](#b-HelloController)

            5.  [1.2.2.5.
                5、在WEB-INF目录下创建pages文件夹，编写success.jsp的成功页面](#5、在WEB-INF目录下创建pages文件夹，编写success-jsp的成功页面)
            6.  [1.2.2.6.
                6、启动Tomcat服务器，进行测试](#6、启动Tomcat服务器，进行测试)

        3.  [1.2.3.
            三、入门案例的执行过程分析](#三、入门案例的执行过程分析)
            1.  [1.2.3.1. 1、入门案例的执行流程](#1、入门案例的执行流程)
            2.  [1.2.3.2.
                2、入门案例中的组件分析](#2、入门案例中的组件分析)
                1.  [1.2.3.2.1. a)
                    DispatcherServlet：前端控制器](#a-DispatcherServlet：前端控制器)
                2.  [1.2.3.2.2. b)
                    HandlerMapping：处理器映射器](#b-HandlerMapping：处理器映射器)
                3.  [1.2.3.2.3. c) Handler：处理器](#c-Handler：处理器)
                4.  [1.2.3.2.4. d)
                    HandlAdapter：处理器适配器（转接口）](#d-HandlAdapter：处理器适配器（转接口）)
                5.  [1.2.3.2.5. e) View
                    Resolver：视图解析器](#e-View-Resolver：视图解析器)
                6.  [1.2.3.2.6. f) View：视图](#f-View：视图)

            3.  [1.2.3.3.
                3、\<mvc:annotation-driven\>说明](#3、-lt-mvc-annotation-driven-gt-说明)

        4.  [1.2.4. 四、RequestMapping注解](#四、RequestMapping注解)
            1.  [1.2.4.1.
                1、RequestMapping注解的作用是建立请求URL和处理方法之间的对应关系](#1、RequestMapping注解的作用是建立请求URL和处理方法之间的对应关系)
            2.  [1.2.4.2.
                2.、RequestMapping注解可以作用在方法和类上：更加清晰](#2-、RequestMapping注解可以作用在方法和类上：更加清晰)
            3.  [1.2.4.3.
                3、RequestMapping的属性](#3、RequestMapping的属性)

    3.  [1.3. part3、请求参数的绑定](#part3、请求参数的绑定)
        1.  [1.3.1. 一、请求参数的绑定说明](#一、请求参数的绑定说明)
            1.  [1.3.1.1. 1、绑定机制](#1、绑定机制)
            2.  [1.3.1.2. 2、支持的数据类型](#2、支持的数据类型)

        2.  [1.3.2.
            二、基本数据类型和字符串类型](#二、基本数据类型和字符串类型)
        3.  [1.3.3. 三、实体类型（JavaBean）](#三、实体类型（JavaBean）)
        4.  [1.3.4. 四、集合属性数据封装](#四、集合属性数据封装)
            1.  [1.3.4.1.
                1、List：JSP页面编写方式：list[0].属性](#1、List：JSP页面编写方式：list-0-属性)
            2.  [1.3.4.2.
                2、Map：map[‘key’].属性](#2、Map：map-‘key’-属性)

        5.  [1.3.5. 五、自定义类型转换器](#五、自定义类型转换器)
        6.  [1.3.6.
            六、在控制器中使用原生的ServletAPI对象：](#六、在控制器中使用原生的ServletAPI对象：)

    4.  [1.4. part4、常用的注解](#part4、常用的注解)
        1.  [1.4.1. 一、RequestParam注解](#一、RequestParam注解)
            1.  [1.4.1.1. 1、作用：](#1、作用：)
            2.  [1.4.1.2. 2、属性：](#2、属性：)

        2.  [1.4.2.
            二、RequestBody注解（异步，json）](#二、RequestBody注解（异步，json）)
            1.  [1.4.2.1. 1、作用：](#1、作用：-1)
            2.  [1.4.2.2. 2、属性：](#2、属性：-1)

        3.  [1.4.3. 三、PathVariable注解](#三、PathVariable注解)
            1.  [1.4.3.1. 1、作用：](#1、作用：-2)
            2.  [1.4.3.2. 2、属性：](#2、属性：-2)
            3.  [1.4.3.3. 3、Restful风格的URL](#3、Restful风格的URL)
                1.  [1.4.3.3.1. a)](#a)
                2.  [1.4.3.3.2. b)
                    restful风格的URL优点:](#b-restful风格的URL优点)
                3.  [1.4.3.3.3. c) restful特性](#c-restful特性)

            4.  [1.4.3.4. 4、实践](#4、实践)

        4.  [1.4.4. 四、基于 HiddentHttpMethodFilter
            的示例（了解即可）](#四、基于-HiddentHttpMethodFilter-的示例（了解即可）)
            1.  [1.4.4.1. 1、作用：](#1、作用：-3)
            2.  [1.4.4.2. 2、使用方法：](#2、使用方法：)
            3.  [1.4.4.3. 3、源码分析：](#3、源码分析：)

        5.  [1.4.5.
            五、RequestHeader注解（一般开发中不怎么用）](#五、RequestHeader注解（一般开发中不怎么用）)
            1.  [1.4.5.1. 1、作用：](#1、作用：-4)
            2.  [1.4.5.2. 2、属性：](#2、属性：-3)
            3.  [1.4.5.3. 3、实践](#3、实践)

        6.  [1.4.6. 六、CookieValue注解](#六、CookieValue注解)
            1.  [1.4.6.1. 1、作用：](#1、作用：-5)
            2.  [1.4.6.2. 2、属性：](#2、属性：-4)
            3.  [1.4.6.3. 3、实践](#3、实践-1)

        7.  [1.4.7. 七、ModelAttribute注解](#七、ModelAttribute注解)
            1.  [1.4.7.1. 1、作用](#1、作用)
            2.  [1.4.7.2. 2、属性：](#2、属性：-5)
            3.  [1.4.7.3. 3、应用场景：](#3、应用场景：)
            4.  [1.4.7.4. 4、实践](#4、实践-1)
                1.  [1.4.7.4.1. a) 方法无返回值：](#a-方法无返回值：)
                2.  [1.4.7.4.2. b) 方法有返回值：](#b-方法有返回值：)

        8.  [1.4.8.
            八、SessionAttributes（复数）](#八、SessionAttributes（复数）)
            1.  [1.4.8.1. 1、作用：](#1、作用：-6)
            2.  [1.4.8.2. 2、属性](#2、属性)
            3.  [1.4.8.3. 3、实践：](#3、实践：)

    5.  [1.5. part5、响应数据和结果视图](#part5、响应数据和结果视图)
        1.  [1.5.1. 一、返回值分类](#一、返回值分类)
            1.  [1.5.1.1. 1、返回字符串](#1、返回字符串)
            2.  [1.5.1.2. 2、返回值是void](#2、返回值是void)
            3.  [1.5.1.3. 3.
                返回值是ModelAndView对象（与返回字符串方式类似）](#3-返回值是ModelAndView对象（与返回字符串方式类似）)

        2.  [1.5.2.
            二、SpringMVC框架提供的转发和重定向](#二、SpringMVC框架提供的转发和重定向)
            1.  [1.5.2.1. 1、forward请求转发](#1、forward请求转发)
            2.  [1.5.2.2. 2、redirect重定向](#2、redirect重定向)

        3.  [1.5.3.
            三、ResponseBody响应json数据](#三、ResponseBody响应json数据)
            1.  [1.5.3.1. 1、DispatcherServlet](#1、DispatcherServlet)
            2.  [1.5.3.2.
                2、使用@RequestBody获取请求体数据（点击查看作用）](#2、使用-RequestBody获取请求体数据（点击查看作用）)
            3.  [1.5.3.3.
                3、使用@RequestBody注解把json的字符串转换成JavaBean的对象](#3、使用-RequestBody注解把json的字符串转换成JavaBean的对象)
            4.  [1.5.3.4.
                4、使用@ResponseBody注解把JavaBean对象转换成json字符串，直接响应](#4、使用-ResponseBody注解把JavaBean对象转换成json字符串，直接响应)

    6.  [1.6.
        part6、SpringMVC实现文件上传](#part6、SpringMVC实现文件上传)
        1.  [1.6.1. 1、传统文件上传的回顾](#1、传统文件上传的回顾)
            1.  [1.6.1.1. a)、必要前提](#a-、必要前提)
            2.  [1.6.1.2. b)、原理分析](#b-、原理分析)
            3.  [1.6.1.3.
                c)、借助第三方组件实现文件上传](#c-、借助第三方组件实现文件上传)
            4.  [1.6.1.4. d)、代码：](#d-、代码：)

        2.  [1.6.2.
            2、SpringMVC传统方式文件上传](#2、SpringMVC传统方式文件上传)
        3.  [1.6.3.
            3、SpringMVC跨服务器方式文件上传](#3、SpringMVC跨服务器方式文件上传)
            1.  [1.6.3.1. 1、搭建图片服务器：](#1、搭建图片服务器：)
            2.  [1.6.3.2.
                2、实现SpringMVC跨服务器方式文件上传](#2、实现SpringMVC跨服务器方式文件上传)

    7.  [1.7. part7、SpringMVC的异常处理](#part7、SpringMVC的异常处理)
        1.  [1.7.1. 1、异常处理思路](#1、异常处理思路)
        2.  [1.7.2. 2、SpringMVC的异常处理](#2、SpringMVC的异常处理)
            1.  [1.7.2.0.1. a)、不进行处理：](#a-、不进行处理：)
            2.  [1.7.2.0.2. b)、异常处理](#b-、异常处理)
                1.  [1.7.2.0.2.1.
                    i)、自定义异常类：继承Exception](#i-、自定义异常类：继承Exception)
                2.  [1.7.2.0.2.2.
                    ii)、自定义异常处理器](#ii-、自定义异常处理器)
                3.  [1.7.2.0.2.3.
                    iii)、配置异常处理器](#iii-、配置异常处理器)
                4.  [1.7.2.0.2.4. iv)、结果](#iv-、结果)

2.  [1.8.
    part8、SpringMVC框架中的拦截器](#part8、SpringMVC框架中的拦截器)
    1.  [1.8.1. 1、拦截器的概述](#1、拦截器的概述)
    2.  [1.8.2. 2、自定义拦截器步骤](#2、自定义拦截器步骤)
    3.  [1.8.3.
        3、HandlerInterceptor接口中的方法](#3、HandlerInterceptor接口中的方法)
    4.  [1.8.4. 4、配置多个拦截器](#4、配置多个拦截器)
    5.  [1.8.5.
        part9、SpringMVC暂告一段落……未完待续……](#part9、SpringMVC暂告一段落……未完待续……)

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
