# spring IOC

## 框架概念

Spring 是众多开源java项目中的一员，基于分层的javaEE应用一站式轻量级开源框架，主要核心是 IOC（控制反转/依赖注入）与 AOP（面向切面）两大技术，实现项目在开发过程中的轻松解耦，提高项 目的开发效率。

 在项目中引入 Spring 立即可以带来下面的好处 降低组件之间的耦合度,实现软件各层之间的解耦。可 以使用容器提供的众多服务，如：事务管理服务、消息服务等等。当我们使用容器管理事务时，开发人 员就不再需要手工控制事务.也不需处理复杂的事务传播。 容器提供单例模式支持，开发人员不再需要 自己编写实现代码。 容器提供了AOP技术，利用它很容易实现如权限拦截、运行期监控等功能。

## Spring 框架环境搭建

### 新建 Maven 项目

### 调整项目环境

1. 修改 JDK 版本

   ```properties
   <properties>
     <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

   

2. 修改单元测试 JUnit 版本

   ```properties
   <dependency>
     <groupId>junit</groupId>
     <artifactId>junit</artifactId>
     <version>4.12</version>
     <scope>test</scope>
   </dependency>
   ```

   

3. build标签中的pluginManagement标签

   ```properties
   <!--删除build标签中的pluginManagement标签-->
   <build>
   </build>
   ```

### 添加 Spring 框架的依赖坐标

Maven仓库：https://mvnrepository.com/

```properties
<!-- 添加Spring框架的核心依赖 -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.4.RELEASE</version>
</dependency>
```

### 编写 Bean 对象

```java
package com.xxxx.service;
public class UserService {
    public void test(){
        System.out.println("Hello Spring!");
   }
}
```

### 添加Spring 配置文件

1.在 src\main\resources 目录下新建 spring.xml 文件，并拷贝官网文档提供的模板内容到 xml 中。

spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
   <!--
        xmlns 即 xml namespace xml使用的命名空间
        xmlns:xsi 即xml schema instance xml 遵守的具体规范
        xsi:schemaLocation 本文档xml遵守的规范 官方指定
   -->
   <bean id="userService" class="com.xxxx.service.UserService"></bean>
</beans>
```

2.在 spring.xml 中配置 Bean 对象

```xml
<!--
 id：bean对象的id，唯一标识。一般是Bean对象的名称的首字母小写
 class：bean对象的类路径
-->
<bean id="userService" class="com.xxxx.service.UserService"></bean>
```

### 加载配置文件，获取实例化对象

```java
package com.xxxx;
import com.xxxx.service.UserService;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class App {
    public static void main(String[] args) {
        // 获取Spring上下文环境 (加载配置文件)
        ApplicationContext ac = new
ClassPathXmlApplicationContext("spring.xml");
        // 通过getBean方法得到Spring容器中实例化好的Bean对象 （实例化Bean对象）
        // userService代表的是配置文件中bean标签的id属性值
        UserService userService = (UserService) ac.getBean("userService");
        // 调用方法 （使用实例化对象）
        userService.test();
   }
}
```

## Spring IOC 配置文件加载

### Spring 配置文件加载

```java
ApplicationContext ac  = new ClassPathXmlApplicationContext("spring.xml");
```

### Spring 多配置文件加载

**可变参数，传入多个文件名**

```java
// 同时加载多个资源文件
ApplicationContext ac = new
ClassPathXmlApplicationContext("spring.xml","dao.xml");
```

**通过总的配置文件import其他配置文件**

spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <!--导入需要包含的资源文件-->
    <import resource="service.xml"/>
    <import resource="dao.xml"/>
</beans>
```

加载时只需加载总的配置文件即可

```java
// 加载总的资源文件
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
```

## Spring IOC 容器 Bean 对象实例化

### 构造器实例化

注：通过默认构造器创建 空构造方法必须存在 否则创建失败

1.  设置配置文件 spring.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
       <bean id="userService" class="com.xxxx.service.UserService"></bean>
   </beans>
   ```

   

2. 获取实例化对象

   ```java
   ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
   UserService userService = (UserService) ac.getBean("userService");  
   userService.test();
   ```

   ### 静态工厂实例化（了解）

   ### 实例化工厂实例化（了解）

### Spring三种实例化Bean的方式比较

- 方式一：通过bean的缺省构造函数创建，当各个bean的业务逻辑相互比较独立的时候或者和外 界关联较少的时候可以使用。 
- 方式二：利用静态factory方法创建，可以统一管理各个bean的创建，如各个bean在创建之前需要 相同的初始化处理，则可用这个factory方法险进行统一的处理等等。 
- 方式三：利用实例化factory方法创建，即将factory方法也作为了业务bean来控制，1可用于集成 其他框架的bean创建管理方法，2能够使bean和factory的角色互换。

!>开发中项目一般使用一种方式实例化bean，项目开发基本采用第一种方式，交给Spring托管，使 用时直接拿来使用即可。另外两种了解

## Spring IOC 注入

### Spring IOC 手动装配（注入）

Spring 支持的注入方式共有四种：set 注入、构造器注入、静态工厂注入、实例化工厂注入。

#### set方法注入

- 属性字段需要提供set方法 
- 四种方式，推荐使用set方法注入

**业务对象 JavaBean**

1. 属性字段提供set方法

   ```java
   public class UserService {
       // 业务对象UserDao set注入（提供set方法）
       private UserDao userDao;
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
      }
   }
   ```

   

2. 配置文件的bean标签设置property标签

   ```java
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
       
      <!--
           IOC通过property标签手动装配（注入）：
               Set方法注入
                   name：bean对象中属性字段的名称
                   ref：指定bean标签的id属性值
       -->
       <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>
    <bean id="userService" class="com.xxxx.service.UserService">
           <!--业务对象 注入-->
           <property name="userDao" ref="userDao"/>
       </bean>
   </beans>
   ```

   **常用对象和基本类型**

#### 构造器注入

- 提供带参构造器

**单个Bean对象作为参数**

Java 代码

```java
public class UserService {
    private UserDao userDao; // JavaBean 对象
    
    public UserService(UserDao userDao) {
        this.userDao = userDao;
   }
    public  void  test(){
        System.out.println("UserService Test...");
        userDao.test();
   }
}
```

XML配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
 <!--
        IOC通过构造器注入：
            通过constructor-arg标签进行注入
                name：属性名称
                ref：指定bean标签的id属性值
    -->
    <bean id="userDao" class="com.xxxx.dao.UserDao" ></bean>
    
    <bean id="userService" class="com.xxxx.service.UserService">
        <constructor-arg name="userDao" ref="userDao"></constructor-arg>
    </bean>
</beans>
```

**多个Bean对象作为参数**

**Bean对象和常用对象作为参数**

**循环依赖问题**

循环问题产生的原因： Bean通过构造器注入，之间彼此相互依赖对方导致bean无法实例化。 

如何解决：将构造器注入改为set方法注入

#### 静态工厂注入

#### 实例化工厂注入

定义工厂类

```java
public class InstanceFactory {
     public TypeDao createTypeDao() {
        return new TypeDao();
   }
}
```

Java代码

```java
public class TypeService {
    private TypeDao typeDao;

    public void setTypeDao(TypeDao typeDao) {
        this.typeDao = typeDao;
   }
    public void  test() {
        System.out.println("TypeService Test...");
   }
}
```

XML配置

声明工厂bean标签，声明bean对象，指明工厂对象和工厂方法

```xml
<bean id="typeService" class="com.xxxx.service.TypeService">
 <property name="typeDao" ref="typeDao"/>
</bean>
<!--
 实例化工厂注入：
 实例化工厂注入也是借助set方法注入，只是被注入的bean对象的实例化是通过实例化工
厂实例化的
-->
<bean id="instanceFactory" class="com.xxxx.factory.InstanceFactory"></bean>
<bean id="typeDao" factory-bean="instanceFactory" factorymethod="createTypeDao"></bean>
```

!>重点掌握set注入和构造器注入，工厂方式了解即可。实际开发中基本使用set方式注入bean。

### Spring IOC 自动装配（注入）

**注解方式注入 Bean**

对于 bean 的注入，除了使用 xml 配置以外，可以使用注解配置。注解的配置，可以简化配置文件， 提高开发的速度，使程序看上去更简洁。对于注解的解释，Spring对于注解有专门的解释器，对定义的 注解进行解析，实现对应bean对象的注入。通过**反射**技术实现

**准备环境**

1. 准备环境

   ```xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          http://www.springframework.org/schema/context/spring-context.xsd">
   ```

   

2. 开启自动化注入

   ```xml
   <!--开启自动化装配（注入）-->
   <context:annotation-config/>
   <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>
   <bean id="userService" class="com.xxxx.service.UserService"></bean>
   ```

   

3. 给注入的bean对象添加注解

   

**@Resource注解**

@Resource注解实现自动注入（反射）

- 默认根据属性字段名称查找对应的bean对象 （属性字段的名称与bean标签的id属性值相等） 
- 如果属性字段名称未找到，则会通过类型（Class类型）查找
- 属性可以提供set方法，也可以不提供set方法 注解可以声明在属性级别 或 set方法级别 
- 可以设置name属性，name属性值必须与bean标签的id属性值一致；如果设置了name属性值， 就只会按照name属性值查找bean对象 
- 当注入接口时，如果接口只有一个实现则正常实例化；如果接口存在多个实现，则需要使用name 属性指定需要被实例化的bean对象

**@Autowired注解**

@Autowired注解实现自动化注入：

默认通过类型（Class类型）查找bean对象 与属性字段的名称无关 

属性可以提供set方法，也可以不提供set方法 

注解可以声明在属性级别 或 set方法级别 

可以添加@Qualifier结合使用，通过value属性值查找bean对象（value属性值必须要设置，且值 

要与bean标签的id属性值对应）

!>推荐使用@Resource 注解是属于J2EE的，减少了与Spring的耦合。

## Spring IOC 扫描器

实际的开发中，bean的数量非常多，采用手动配置bean的方式已无法满足生产需要，Spring这时候 同样提供了扫描的方式，对扫描到的bean对象统一进行管理，简化开发配置，提高开发效率。

### Spring IOC 扫描器的配置

1. 设置自动化扫描的范围

   如果bean对象未在指定包范围，即使声明了注解，也无法实例化

2. 使用指定的注解（声明在类级别）  bean对象的id属性默认是 类的首字母小写

   Dao层：       @Repository     

   Service层：       @Service     

   Controller层：       @Controller     

   任意类：       @Component

   

设置自动化扫描的范围

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 设置自动化扫描的范围 -->
    <context:component-scan base-package="com.xxxx"/>
</beans>
```

使用特定的注解

## Bean的作用域与生命周期

### Bean的作用域

默认情况下，我们从Spring容器中拿到的对象均是单例的，对于bean的作用域类型如下：

**singleton 作用域**

![](D:\Users\17482\Desktop\docify_file\docs\springioc\README.assets\Snipaste_2022-05-11_21-36-57-16522763025612.png)

**prototype 作用域**

### Bean的生命周期

对比已经学过的servlet 生命周期（容器启动装载并实例化servlet类，初始化servlet，调用service方 法，销毁servlet）。

同样对于Spring容器管理的bean也存在生命周期的概念

在Spring中，Bean的生命周期包括Bean的定义、初始化、使用和销毁4个阶段