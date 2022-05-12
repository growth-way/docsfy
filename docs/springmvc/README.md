# SpringMVC

## 什么叫MVC？

 模型-视图-控制器（MVC）是一个众所周知的以设计界面应用程序为基础的设计思想。它主要通过 分离模型、视图及控制器在应用程序中的角色将业务逻辑从界面中解耦。通常，模型负责封装应用程序 数据在视图层展示。视图仅仅只是展示这些数据，不包含任何业务逻辑。控制器负责接收来自用户的请 求，并调用后台服务（service或者dao）来处理业务逻辑。处理后，后台业务层可能会返回了一些数据 在视图层展示。控制器收集这些数据及准备模型在视图层展示。MVC模式的核心思想是将业务逻辑从界 面中分离出来，允许它们单独改变而不会相互影响。

## Spring MVC是什么?

Spring MVC是Spring家族中的一个web成员, 它是一种基于Java的实现了Web MVC设计思想的请求 驱动类型的轻量级Web框架，即使用了MVC架构模式的思想，将web层进行职责解耦，基于请求驱动指 的就是使用请求-响应模型，框架的目的就是帮助我们简化开发，Spring MVC也是要简化我们日常Web 开发的。

 Spring MVC是服务到工作者思想的实现。前端控制器是DispatcherServlet；应用控制器拆为处理 器映射器(Handler Mapping)进行处理器管理和视图解析器(View Resolver)进行视图管理；支持本地化/ 国际化（Locale）解析及文件上传等；提供了非常灵活的数据验证、格式化和数据绑定机制；提供了强 大的约定大于配置（惯例优先原则）的契约式编程支持。

## Spring MVC能帮我们做什么?

1. 让我们能非常简单的设计出干净的Web层； 
2. 进行更简洁的Web层的开发； 
3. 天生与Spring框架集成（如IoC容器、AOP等）； 
4. 提供强大的约定大于配置的契约式编程支持； 
5. 能简单的进行Web层的单元测试；
6. 支持灵活的URL到页面控制器的映射；
7. 非常容易与其他视图技术集成，如jsp、Velocity、FreeMarker等等，因为模型数据不放在特定的 API里，而是放在一个Model里（Map数据结构实现，因此很容易被其他框架使用）；
8. 非常灵活的数据验证、格式化和数据绑定机制，能使用任何对象进行数据绑定，不必实现特定框架 的API； 9. 
9. 支持灵活的本地化等解析；
10. 更加简单的异常处理；
11. 对静态资源的支持；
12. 支持Restful风格。

## SpringMvc 请求流程 & 环境搭建与测试

![](https://img2020.cnblogs.com/blog/1230003/202006/1230003-20200615203107932-1811109468.png)

流程说明

第⼀步：⽤户发送请求⾄前端控制器DispatcherServlet

第⼆步： DispatcherServlet收到请求调⽤HandlerMapping处理器映射器

第三步：处理器映射器根据请求Url找到具体的Handler（后端控制器），⽣成处理器对象及处理器拦截器(如果 有则⽣成)⼀并返回DispatcherServlet

第四步： DispatcherServlet调⽤HandlerAdapter处理器适配器去调⽤Handler

第五步：处理器适配器执⾏Handler

第六步： Handler执⾏完成给处理器适配器返回ModelAndView

第七步：处理器适配器向前端控制器返回 ModelAndView， ModelAndView 是SpringMVC 框架的⼀个底层对 象，包括 Model 和 View

第⼋步：前端控制器请求视图解析器去进⾏视图解析，根据逻辑视图名来解析真正的视图。

第九步：视图解析器向前端控制器返回View

第⼗步：前端控制器进⾏视图渲染，就是将模型数据（在 ModelAndView 对象中）填充到 request 域

第⼗⼀步：前端控制器向⽤户响应结果

### Spring MVC优势

### Spring Mvc 环境搭建与测试

**新建Maven webApp**

**pom.xml 坐标添加**

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
  <dependencies>
    <!-- spring web -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <!-- spring mvc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <!-- web servlet -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.0.1</version>
    </dependency>
  </dependencies>
<build>
<plugins>
            <!-- 编译环境插件 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
			<plugin>
                <groupId>org.mortbay.jetty</groupId>
                <artifactId>maven-jetty-plugin</artifactId>
                <version>6.1.25</version>
                <configuration>
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <contextPath>/springmvc01</contextPath>
                </configuration>
            </plugin>
        </plugins>
</build>

```

**配置web.xm**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app id="WebApp_ID" version="3.0"
    xmlns="http://java.sun.com/xml/ns/javaee"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
    http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">    
    <!-- 编码过滤 utf-8 -->
    <filter>
        <description>char encoding filter</description>
        <filter-name>encodingFilter</filter-name>
        <filterclass>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <!-- servlet请求分发器 -->
    <servlet>
        <servlet-name>springMvc</servlet-name>
        <servletclass>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:servlet-context.xml</param-value>
        </init-param>
        <!-- 表示启动容器时初始化该Servlet -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springMvc</servlet-name>
        <!-- 这是拦截请求, /代表拦截所有请求,拦截所有.do请求 -->
        <url-pattern>*.do</url-pattern>
    </servlet-mapping>
</web-app> 
```

要想启动我们的springMvc 环境，目前对于mvc 框架的配置还未进行。以上在web.xml中引用了servlet-context.xml 文件

**servlet-context.xml**

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <context:component-scan base-package="com.xxxx.springmvc.controller">
</context:component-scan>
    <mvc:annotation-driven/>
    <!--配置视图解析器 默认的视图解析器- -->
    <bean id="defaultViewResolver"
        
class="org.springframework.web.servlet.view.InternalResourceViewResolver">
      <property name="viewClass"
value="org.springframework.web.servlet.view.JstlView" />
      <property name="contentType" value="text/html" />
      <property name="prefix" value="/WEB-INF/jsp/" />
      <property name="suffix" value=".jsp" />
    </bean>
</beans>
```

**页面控制器的编写**

```java
@Controller
public class HelloController {
    
    /**
     * 请求映射地址 /hello.do
     * @return
     */
    @RequestMapping(value={"/hello","asdasdas","asfs"})
    public ModelAndView hello(){
        ModelAndView mv=new ModelAndView();
        mv.addObject("hello", "hello spring mvc");
        mv.setViewName("hello");
        return mv;  
   }
}
```

**添加视图页面**

在WEB-INF 下新建jsp文件夹 ，并在文件加下新建hello.jsp

```jsp
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath =
request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+pa
th+"/";
%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    <title>My JSP 'hello.jsp' starting page</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">    
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
  </head>
  <body>
  <!-- el表达式接收参数值 -->
   ${hello}
  </body>
</html>
```

## URL地址映射配置 & 参数绑定

### URL 映射地址配置之@RequestMapping

在类前面定义，则将url和类绑定,在方法前面定义，则将url和类的方法绑定

```java
//url: http://localhost:8080/springmvc01/hello2/test01.do
@RequestMapping("test01")
public ModelAndView test01(){
  ModelAndView mv=new ModelAndView();
  mv.setViewName("hello");
  mv.addObject("hello", "hello test01");
  return mv;
}
```

### 参数绑定

请求参数到处理器功能处理方法的方法参数上的绑定，对于参数绑定非常灵活

**基本数据类型、字符串数据绑定**

```java
/**
* 简单数据类型 值必须存在 不传可以通过默认值代替
*/
@RequestMapping("data1")
public void data1(@RequestParam(defaultValue="10",name="age")int age,
        @RequestParam(defaultValue="1",name="flag")boolean flag,
        @RequestParam(defaultValue="100",name="s")double s){
    System.err.println("age:"+age+":flag:"+flag+":s:"+s);
}
/**
* 包装类型 值可以为空
*/
@RequestMapping("data2")
public void data2(Integer age,Double s){
    System.err.println("age:"+age+":s:"+s);
}
/**
* 字符串注入
* @param str
*/
@RequestMapping("data3")
public void data3(String str){
    System.err.println("str:"+str);
}

```

**数组类型**

```java
@RequestMapping("/dataTest3")
public void getParamsData3(@RequestParam(value="ids")String[] ids){
    for(String id:ids){
        System.out.println(id+"---");
   }
}
```

**vo 类型**

```java
@RequestMapping("/dataTest4")
public void getParamsData4(User user){
    System.out.println(user);
}
```

**list 类型**

此时user 实体需要定义list 属性

```java
public class User {
    private int id;
    private String userName;
    private String userPwd;
    
    private List<Phone> phones=new ArrayList<Phone>();
}
```

Jsp 页面定义

```jsp
<form action="dataTest5.do" method="post">
    <input name="phones[0].num" value="123456" />
    <input name="phones[1].num" value="4576" />
    <button type="submit"> 提交</button>
</form>
```

Controller 方法

```java
@RequestMapping("/dataTest5")
public void getParamsData5(User user){
System.out.println(user);
}
```

**Set 类型**

Set和List类似，也需要绑定在对象上，而不能直接写在Controller方法的参数中。但是，绑定Set数 据时，必须先在Set对象中add相应的数量的模型对象。

**Map 类型数据**

Map最为灵活，它也需要绑定在对象上，而不能直接写在Controller方法的参数中。

```java
public class User {
    private int id;
    private String userName;
    private String userPwd;
    
    private Set<Phone> phones=new HashSet<Phone>();
    
    private Map<String, Phone> map=new HashMap<String, Phone>();
    public User() {
        phones.add(new Phone());
        phones.add(new Phone());
        phones.add(new Phone());
   }
}
```

Controller 方法

```java
@RequestMapping("/dataTest7")
public void getParamsData7(User user){
    Set<Entry<String, Phone>>  set=user.getMap().entrySet();
    for(Entry<String, Phone> entry:set){
        System.out.println(entry.getKey()+"--"+entry.getValue().getNum());
        
   }  
}
```

表单页面

```jsp
<form action="dataTest7.do" method="post">
   <input name="map['1'].num" value="123456" />
   <input name="map['2'].num" value="4576" />
   <input name="map['3'].num" value="4576" />
   <button type="submit"> 提交</button>
</form>
```

## 请求转发与重定向的问题

SpringMvc 默认采用服务器内部转发的形式展示页面信息。同样也支持重定向页面。

### 转发与重定向代码实现

```java
/**
* 重定向到 jsp 中文会出现乱码
*/
@RequestMapping("/queryView1")
public String queryView1(){
    return "redirect:v1.jsp?a=admin&b=123456";
}
/**
* 重定向到 jsp 中文乱码解决
*/
@RequestMapping("/queryView3")
public String queryView3(RedirectAttributes attr){
    attr.addAttribute("a", "admin");
    attr.addAttribute("b", "奥利给");
    return "redirect:v1.jsp";
}
/**
* 重定向到 jsp ModelAndView1
*/
@RequestMapping("/queryView4")
public ModelAndView queryView4(RedirectAttributes attr){
    
    ModelAndView mv=new ModelAndView();
    attr.addAttribute("a", "admin");
    attr.addAttribute("b", "奥利给");
    mv.setViewName("redirect:v1.jsp");
    return mv;
}
/**
* 重定向到 jsp ModelAndView2 mv 携带参数
*/
@RequestMapping("/queryView5")
public ModelAndView queryView5(){
    
    ModelAndView mv=new ModelAndView();
    mv.setViewName("redirect:v1.jsp");
    mv.addObject("a", "admin");
    mv.addObject("b", "奥利给");
    System.out.println("重定向。。。");
    return mv;
}
/**
* 重定向到Controller 并传递参数
*/
@RequestMapping("/queryView6")
public String queryView6(RedirectAttributes attr){
    attr.addAttribute("a", "admin");
    attr.addAttribute("b", "奥利给");
    return "redirect:/user/queryUserById.do";
}
/**
* 重定向到Controller modelandview
* @return
*/
@RequestMapping("/queryView7")
public ModelAndView queryView7(){
    ModelAndView mv=new ModelAndView();
    mv.setViewName("redirect:/user/queryUserById.do");
    mv.addObject("a", "admin");
    mv.addObject("b", "奥利给");
    return mv;
}
重定向页面值获取  ${param.a}|||${param.b}
/**
     * 转发到视图
     */
@RequestMapping("/queryView8")
public ModelAndView queryView8(){
    ModelAndView mv=new ModelAndView();
    mv.setViewName("v1");
    mv.addObject("a", "admin");
    mv.addObject("b", "奥利给");
    return mv;
}
/**
* 转发到controller
*/
@RequestMapping("/queryView9")
public ModelAndView queryView9(HttpServletRequest request){
    ModelAndView mv=new ModelAndView();
    mv.setViewName("forward:user/queryUserById2.do?a=admin&b=奥利给");
    return mv;
}
页面值获取 ${a}||${b}
```

## SpringMvc 之Json数据开发

### 基本概念

Json在企业开发中已经作为通用的接口参数类型，在页面（客户端）解析很方便。SpringMvc 对于json 提供了良好的支持，这里需要修改相关配置，添加json数据支持功能

### @ResponseBody

该注解用于将Controller的方法返回的对象，通过适当的HttpMessageConverter转换为指定格式 后，写入到Response对象的body数据区。 返回的数据不是html标签的页面，而是其他某种格式的数据时（如json、xml等）使用（通常用于ajax 请求）

### @RequestBody

该注解用于读取Request请求的body部分数据，使用系统默认配置的HttpMessageConverter进行 解析，然后把相应的数据绑定到要返回的对象上 ,再把HttpMessageConverter返回的对象数据绑定到 controller中方法的参数上。

##  拦截器

### 基本概念

SpringMVC 中的Interceptor 拦截器也是相当重要和相当有用的，它的主要作用是拦截用户的请求并进 行相应的处理。比如通过它来进行权限验证，或者是来判断用户是否登陆等操作。对于springmvc拦截 器的定义方式有两种方式:

实现接口：org.springframework.web.servlet.HandlerInterceptor 

继承适配器org.springframework.web.servlet.handler.HandlerInterceptorAdapter

### 拦截器实现

#### **实现HandlerInterceptor 接口**

```java
public class MyInterceptor1 implements HandlerInterceptor{
    /**
     * preHandle 在请求方法拦截前执行
     * 返回true 代表对当前请求进行放行处理
     */
    @Override
    public boolean preHandle(HttpServletRequest request,
            HttpServletResponse response, Object handler) throws Exception {
        System.out.println("handler方法之前执行MyInterceptor1-->preHandle方法...");
        return true;  //继续执行action
   }
    /**
     * 请求执行后，生成视图前执行
     */
    @Override
    public void postHandle(HttpServletRequest request,
            HttpServletResponse response, Object handler,
            ModelAndView modelAndView) throws Exception {
			System.out.println("handler方法之后，生成视图之前执行MyInterceptor1-->postHandle方法...");  
   }
    /**
     * 在请求方法执行后进行拦截
     */
    @Override
    public void afterCompletion(HttpServletRequest request,
            HttpServletResponse response, Object handler, Exception ex)
            throws Exception {
        
        System.out.println("handler方法执行完毕，生成视图后执行MyInterceptor1--
>afterCompletion...");
   }
}
```

**生效拦截器xml配置**

```xml
<!--配置方式一-->
<mvc:interceptors>
    <!-- 使用bean定义一个Interceptor
    直接定义在mvc:interceptors根下面的Interceptor将拦截所有的请求 -->
    <bean class="com.xxxx.springmvc.interceptors.MyInterceptor1" />
</mvc:interceptors>
```

```xml
<!--配置方式二-->
<mvc:interceptors>
    <!-- 定义在 mvc:interceptor 下面 拦截所有test地址开头的请求-->
    <mvc:interceptor>
        <mvc:mapping path="/test/*.do" />
        <bean class="com.xxxx.springmvc.interceptors.MyInterceptor1" />
    </mvc:interceptor>
</mvc:interceptors>
```

#### 继承HandlerInterceptorAdapter

实际上最终还是HandlerInterceptor接口实现。

```java
public class MyInterceptor2 extends HandlerInterceptorAdapter{
    /**
     * 重写preHandle 请求执行前执行
     */
    @Override
    public boolean preHandle(HttpServletRequest request,
            HttpServletResponse response, Object handler) throws Exception {
        System.out.println("handler方法之前执行MyInterceptor2-->preHandle方法...");
        return true;
   }
}
```

**生效拦截器xml配置**

```xml
<!--配置方式二-->
<mvc:interceptors>
    <!-- 定义在 mvc:interceptor 下面 拦截所有test地址开头的请求-->
    <mvc:interceptor>
        <mvc:mapping path="/test/*.do" />
        <bean class="com.xxxx.springmvc.interceptors.MyInterceptor2" />
    </mvc:interceptor>
</mvc:interceptors>
```

#### 多个拦截器实现

SpringMvc 框架支持多个拦截器配置，从而构成拦截器链，对客户端请求进行多次拦截操作。

### 拦截器应用-非法请求拦截处理

## SpringMvc文件上传

## SSM框架集成与测试

### 环境配置

#### 创建maven web 工程ssm

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
</properties>
<dependencies>
    <!-- junit 测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- spring 核心jar -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.2.RELEASE</version>
    </dependency>
    <!-- spring 测试jar -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>4.3.2.RELEASE</version>
    </dependency>
    <!-- spring jdbc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>4.3.2.RELEASE</version>
    </dependency>
    <!-- spring事物 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-tx</artifactId>
        <version>4.3.2.RELEASE</version>
    </dependency>
<!-- aspectj切面编程的jar -->
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.8.9</version>
    </dependency>
    <!-- c3p0 连接池 -->
    <dependency>
        <groupId>c3p0</groupId>
        <artifactId>c3p0</artifactId>
        <version>0.9.1.2</version>
    </dependency>
    <!-- mybatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.1</version>
    </dependency>
    <!-- 添加mybatis与Spring整合的核心包 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.0</version>
    </dependency>
    <!-- mysql 驱动包 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.39</version>
    </dependency>
    <!-- 日志打印相关的jar -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.7.2</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.2</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper -->
    <dependency>
        <groupId>com.github.pagehelper</groupId>
        <artifactId>pagehelper</artifactId>
        <version>5.1.10</version>
    </dependency>
    <!-- spring web -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
<version>4.3.2.RELEASE</version>
    </dependency>
    <!-- spring mvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>4.3.2.RELEASE</version>
    </dependency>
    <!-- web servlet -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.0.1</version>
    </dependency>
    <!-- 添加json 依赖jar包 -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-core</artifactId>
        <version>2.7.0</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.7.0</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-annotations</artifactId>
        <version>2.7.0</version>
    </dependency>
    <dependency>
        <groupId>commons-fileupload</groupId>
        <artifactId>commons-fileupload</artifactId>
        <version>1.3.2</version>
    </dependency>
</dependencies>
<build>
        <finalName>ssm</finalName>
        <!--
 Maven 项目:如果源代码(src/main/java)存在xml、properties、tld 等文件  
 Maven 默认不会自动编译该文件到输出目录,如果要编译源代码中xml properties tld
等文件  
 需要显式配置resources 标签
         -->
        <resources>
            <resource>
                <directory>src/main/resources</directory>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                    <include>**/*.properties</include>
                    <include>**/*.tld</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.mortbay.jetty</groupId>
                <artifactId>maven-jetty-plugin</artifactId>
                <version>6.1.25</version>
                <configuration>
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <contextPath>/ssm</contextPath>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

#### web.xml 文件修改

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://java.sun.com/xml/ns/javaee"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
    id="WebApp_ID" version="3.0">
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring.xml</param-value>
    </context-param>
    <listener>
        <listener-class>
           org.springframework.web.context.ContextLoaderListener
        </listener-class>
    </listener>
    <filter>
        <description>char encoding filter</description>
        <filter-name>encodingFilter</filter-name>
        <filter-class>
           org.springframework.web.filter.CharacterEncodingFilter</filterclass>
           <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <servlet>
        <servlet-name>springMvc</servlet-name>
        <servletclass>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:servlet-context.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springMvc</servlet-name>
        <url-pattern>*.do</url-pattern>
    </servlet-mapping>
</web-app>
```

#### servlet-context.xml添加

src/main/resources 下创建servelt-context.xml 内容如下:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 扫描com.springmvc.crm 下包 -->
    <context:component-scan base-package="com.xxxx.ssm.controller" />
    <!-- mvc 注解驱动 并添加json 支持 -->
    <mvc:annotation-driven>
        <mvc:message-converters>
            <!-- 返回信息为字符串时 处理 -->
            <bean
class="org.springframework.http.converter.StringHttpMessageConverter"/>
            <!-- 将对象转换为json 对象 -->
            <bean
class="org.springframework.http.converter.json.MappingJackson2HttpMessageConvert
er"/>
        </mvc:message-converters>
    </mvc:annotation-driven>
    <!-- 静态资源文件的处理放行 -->
     <mvc:default-servlet-handler />
    
    
     <!--配置视图解析器 默认的视图解析器- -->
    <bean id="defaultViewResolver"
        
class="org.springframework.web.servlet.view.InternalResourceViewResolver">
      <property name="viewClass"
value="org.springframework.web.servlet.view.JstlView" />
      <property name="contentType" value="text/html" />
      <property name="prefix" value="/WEB-INF/jsp/" />
      <property name="suffix" value=".jsp" />
    </bean>
    
    <!-- 文件上传配置 -->
    <bean id="multipartResolver"
      
class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxUploadSize">
            <value>104857600</value>
        </property>
        <property name="maxInMemorySize">
            <value>4096</value>
        </property>
    </bean>
</beans>
```

#### spring.xml配置

src/main/resources 下创建spring.xml 内容如下:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">
    <!-- 扫描基本包 过滤controller层 -->
    <context:component-scan base-package="com.xxxx.ssm" >
    <context:exclude-filter type="annotation"
            expression="org.springframework.stereotype.Controller" />  
    </context:component-scan>
    <!-- 加载properties 配置文件 -->
    <context:property-placeholder location="classpath:db.properties" />
    <aop:aspectj-autoproxy /><!-- aop -->
    <!-- 配置c3p0 数据源 -->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${driver}"></property>
        <property name="jdbcUrl" value="${url}"></property>
        <property name="user" value="${user}"></property>
        <property name="password" value="${password}"></property>
    </bean>
    <!-- 配置事务管理器 -->
    <bean id="txManager"
      
class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!-- 设置事物增强 -->
    <tx:advice id="txAdvice" transaction-manager="txManager">
        <tx:attributes>
            <tx:method name="add*" propagation="REQUIRED" />
            <tx:method name="insert*" propagation="REQUIRED" />
            <tx:method name="update*" propagation="REQUIRED" />
            <tx:method name="delete*" propagation="REQUIRED" />
        </tx:attributes>
    </tx:advice>
    <!-- aop 切面配置 -->
    <aop:config>
        <aop:pointcut id="servicePointcut"
            expression="execution(* com.xxxx.ssm.service..*.*(..))" />
        <aop:advisor advice-ref="txAdvice" pointcut-ref="servicePointcut" />
    </aop:config>
    <!-- 配置 sqlSessionFactory -->
    <bean id="sqlSessionFactory"
class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"></property>
        <property name="configLocation" value="classpath:mybatis.xml" />
        <property name="mapperLocations"
value="classpath:com/xxxx/ssm/mapper/*.xml" />
    </bean>
    
    <!-- 配置扫描器 -->
    <bean id="mapperScanner"
class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!-- 扫描com.springmvc.dao这个包以及它的子包下的所有映射接口类 -->
        <property name="basePackage" value="com.xxxx.ssm.dao" />
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory" />
    </bean>
</beans>
```

####  mybatis.xml全局文件配置

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.xxxx.ssm.vo"/>
    </typeAliases>
    <plugins>
        <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
    </plugins>
</configuration>
```

#### 准备db.properties 文件

src/main/resources 下创建db.properties 内容如下(mysql 创建数据库ssm):

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/ssm?useUnicode=true&characterEncoding=utf8
jdbc.username=root
jdbc.password=root
```

#### 添加log4j.properties 日志打印文件

src/main/resources 下创建log4j.properties 内容如下

```properties
log4j.rootLogger=DEBUG, Console  
#Console
log4j.appender.Console=org.apache.log4j.ConsoleAppender  
log4j.appender.Console.layout=org.apache.log4j.PatternLayout  
log4j.appender.Console.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n  
log4j.logger.java.sql.ResultSet=INFO  
log4j.logger.org.apache=INFO  
log4j.logger.java.sql.Connection=DEBUG  
log4j.logger.java.sql.Statement=DEBUG  
log4j.logger.java.sql.PreparedStatement=DEBUG
```

###  添加源代码

src/main/java 下创建 com.xxxx.ssm.controller、com.xxxx.ssm.service、com.xxxx.ssm.mapper、com.xxxx.ssm.dao、 com.xxxx.ssm.vo等包结构。

#### 添加HelloController.java

```java
@Controller
public class HelloController {
    /**
     * 注入service 层userService 接口
     */
    @Autowired
    private UserService userService;
    @RequestMapping("/hello")
    public ModelAndView hello(){
        ModelAndView mv=new ModelAndView();
        /**
         * 调用service 层查询方法
         */
        User user=userService.queryUserById(7);
        System.out.println(user);
        mv.addObject("user", user);
        mv.setViewName("hello");
        return mv;
   }
}
```

#### 添加UserService.java,提供用户详情查询方法

```java
@Service
public class UserService{
    @Autowired
    private UserMapper userMapper;
    public  User queryUserByUserId(Integer userId){
        return  userMapper.queryUserByUserId(userId);
   }
}
```

#### 添加User.java 文件

#### 添加UserMapper.java 接口文件 ,提供用户详情查询方法

com.xxxx.ssm.dao 包下创建UserMapper.java 文件

```java
public interface UserMapper {
    User queryUserByUserId(Integer userId);
}
```

#### 添加UserMapper.xml 映射文件，提供select 查询标签配置

com.xxxx.ssm.mapper 包下创建UserMapper.xml 文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.xxxx.ssm.dao.AccountDao" >
  <resultMap id="BaseResultMap" type="com.xxxx.ssm.vo.Account" >
    <id column="id" property="id" jdbcType="INTEGER" />
    <result column="aname" property="aname" jdbcType="VARCHAR" />
    <result column="type" property="type" jdbcType="VARCHAR" />
    <result column="money" property="money" jdbcType="DOUBLE" />
    <result column="user_id" property="userId" jdbcType="INTEGER" />
    <result column="create_time" property="createTime" jdbcType="DATE" />
    <result column="update_time" property="updateTime" jdbcType="DATE" />
    <result column="remark" property="remark" jdbcType="VARCHAR" />
  </resultMap>
  <sql id="Base_Column_List" >
    id, aname, type, money, user_id, create_time, update_time, remark
  </sql>
  <select id="selectById" resultMap="BaseResultMap" parameterType="java.lang.Integer" >
    select 
    <include refid="Base_Column_List" />
    from account
    where id = #{id,jdbcType=INTEGER}
  </select>
</mapper>
```

## RestFul URL

## SpringMVC 全局异常统一处理

### 异常处理实现

实现 HandlerExceptionResolver 接口

```java
public class MyExceptionHandler implements HandlerExceptionResolver {
    @Override
    public ModelAndView resolveException(HttpServletRequest request,
            HttpServletResponse response, Object handler, Exception ex) {
        Map<String,Object> map=new HashMap<String, Object>();
        map.put("ex", ex);
        ModelAndView mv=null;
        if(ex instanceof ParamsException){
            return new ModelAndView("error_param", map);
       }
        if(ex instanceof BusinessException){
            return new ModelAndView("error_business", map);
       }
        return new ModelAndView("error", map);
   }
}
```

使用实现 HandlerExceptionResolver 接口的异常处理器进行异常处理，具有集成简单、有良好的扩展 性、对已有代码没有入侵性等优点，同时，在异常处理时能获取导致出现异常的对象，有利于提供更详 细的异常处理信息。