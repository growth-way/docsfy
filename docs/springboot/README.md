# SpringBoot

## Spring Boot快速入门

### 创建Maven 普通项目

```xml
<parent>
 <groupId>org.springframework.boot</groupId>
 <artifactId>spring-boot-starter-parent</artifactId>
 <version>2.2.2.RELEASE</version>
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>

<plugin>
 <groupId>org.springframework.boot</groupId>
 <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```

### 添加源代码

### 创建启动程序

```java
@SpringBootApplication
public class StarterApplication
{
    public static void main(String[] args) {
        SpringApplication.run(Starter.class);
   }
}
```

### Spring Boot 配置文件

application.yml 文件

```yml
## 端口号 上下文路径
server:
 port: 8989
 servlet:
   context-path: /mvc
## 数据源配置
spring:
 datasource:
   type: com.mchange.v2.c3p0.ComboPooledDataSource
   driver-class-name: com.mysql.cj.jdbc.Driver
   url: jdbc:mysql://127.0.0.1:3306/hr
   username: root
   password: root
```

### Freemarker 视图技术集成

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-freemarker</artifactId>
</dependency>

```

```yml
spring:
 freemarker:
   suffix: .ftl
   content-type: text/html
   charset: UTF-8
   template-loader-path: classpath:/views/
```

编写IndexController 控制器转发视图

## Mybatis整合&数据访问

### SpringBoot 整合Mybatis

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
</properties>
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.2.2.RELEASE</version>
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId
<!--
          mybatis 集成
        -->
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>2.1.1</version>
    </dependency>
    <!-- springboot分页插件 -->
    <dependency>
        <groupId>com.github.pagehelper</groupId>
        <artifactId>pagehelper-spring-boot-starter</artifactId>
        <version>1.2.13</version>
    </dependency>
<!--mysql 驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
      
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
    <dependency>
        <groupId>com.mchange</groupId>
        <artifactId>c3p0</artifactId>
        <version>0.9.5.5</version>
    </dependency>
</dependencies>
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build> 
```

**application.yml 整合配置**

```yml
## 端口号
server:
 port: 9999
## 数据源配置
spring:
 datasource:
   type: com.mchange.v2.c3p0.ComboPooledDataSource
   driver-class-name: com.mysql.cj.jdbc.Driver
   url: jdbc:mysql://127.0.0.1:3306/springboot_mybatis?
useUnicode=true&characterEncoding=utf8&serverTimezone=GMT%2B8
   username: root
   password: root
## mybatis 配置
mybatis:
 mapper-locations: classpath:/mappers/*.xml
 type-aliases-package: com.xxxx.springboot.vo
 configuration:
    ## 下划线转驼峰配置
   map-underscore-to-camel-case: true
## pageHelper
pagehelper:
 helper-dialect: mysql
  
#显示dao 执行sql语句
logging:
 level:
   com:
     xxxx:
       springboot:
         dao: debug
```

**源代码添加**

com.xxxx.springboot.dao 包下创建UserDao.java 接口声明查询方法

```java
package com.xxxx.springboot.dao;
import com.xxxx.springboot.vo.User;
public interface UserMapper {
 // 根据用户名查询用户记录
    User queryUserByUserName(String userName);
}
```

resources/mappers 目录下添加UserMapper.xml 配置查询statetment

```cml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.xxxx.springboot.dao.UserMapper">
    <select id="queryUserByUserName" parameterType="string"
resultType="com.xxxx.springboot.vo.User">
       select
       id,user_name,user_pwd
       from t_user
       where user_name=#{userName}
    </select>
</mapper>
```

添加service 、controller 对应代码

添加应用启动入口

```java
@SpringBootApplication
@MapperScan("com.xxxx.springboot.dao")
public class Starter {
    public static void main(String[] args) {
        SpringApplication.run(Starter.class);
   }
}
```

## SpringBoot数据访问操作

完成SpringBoot 与Mybatis 集成后，接下来以用户表为例实现一套用户模块基本数据维护。

```java
public class AssertUtil {
    public  static void isTrue(Boolean flag, String msg){
        if(flag){
            throw  new ParamsException(msg);
        }
    }
}
```

```java
public class ParamsException extends RuntimeException {
    private Integer code=300;
    private String msg="参数异常!";


    public ParamsException() {
        super("参数异常!");
    }

    public ParamsException(String msg) {
        super(msg);
        this.msg = msg;
    }

    public ParamsException(Integer code) {
        super("参数异常!");
        this.code = code;
    }

    public ParamsException(Integer code, String msg) {
        super(msg);
        this.code = code;
        this.msg = msg;
    }

    public Integer getCode() {
        return code;
    }

    public void setCode(Integer code) {
        this.code = code;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }
}
```

### 代码生成

generatorConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>

    <!--
        数据库驱动
            在左侧project边栏的External Libraries中找到mysql的驱动，右键选择copy path
    -->
    <classPathEntry  location="/Users/ls/Documents/Java/Maven/m2/repository/mysql/mysql-connector-java/8.0.18/mysql-connector-java-8.0.18.jar"/>

    <context id="DB2Tables" targetRuntime="MyBatis3">

        <commentGenerator>
            <!-- 是否去除日期那行注释 -->
            <property name="suppressDate" value="true"/>
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>

        <!-- 数据库链接地址账号密码 -->
        <jdbcConnection
                driverClass="com.mysql.cj.jdbc.Driver"
                connectionURL="jdbc:mysql://127.0.0.1:3306/crm?serverTimezone=GMT%2B8"
                userId="root"
                password="root1234">
        </jdbcConnection>

        <!--
             java类型处理器
                用于处理DB中的类型到Java中的类型，默认使用JavaTypeResolverDefaultImpl；
                注意一点，默认会先尝试使用Integer，Long，Short等来对应DECIMAL和NUMERIC数据类型；
                true：使用 BigDecimal对应DECIMAL和NUMERIC数据类型
                false：默认，把JDBC DECIMAL和NUMERIC类型解析为Integer
        -->
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>



        <!-- 生成Model类存放位置 -->
        <javaModelGenerator targetPackage="com.xxxx.crm.vo" targetProject="src/main/java">
            <!-- 在targetPackage的基础上，根据数据库的schema再生成一层package，最终生成的类放在这个package下，默认为false -->
            <property name="enableSubPackages" value="true"/>
            <!-- 设置是否在getter方法中，对String类型字段调用trim()方法 -->
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>


        <!--生成映射文件存放位置-->
        <sqlMapGenerator targetPackage="mappers" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>


        <!--生成Dao类存放位置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.xxxx.crm.dao" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>



        <table tableName="t_customer_serve" domainObjectName="CustomerServe"
               enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false"></table>

    </context>
</generatorConfiguration>
```

命令：mybatis-generator:generate -e



### SpringBoot单元测试

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
</dependency>
```

#### Service业务方法测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest(classes = {Starter.class})
public class TestUserService {
    private Logger log = LoggerFactory.getLogger(TestUserService.class);
    @Resource
    private UserService userService;
    @Before
    public void before(){
        log.info("单元测试开始...");
   }
    @Test
    public  void test01(){
        log.info(userService.queryUserByUserId(10).toString());
   }
    @Test
    public  void test02(){
        log.info(userService.queryUserByParams(new UserQuery()).toString());
   }
    @After
    public void after(){
        log.info("单元测试结束...");
   }
}
```

#### 控制层接口方法测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest(classes = {Starter.class})
@AutoConfigureMockMvc
public class TestUserController {
    private Logger log = LoggerFactory.getLogger(TestUserController.class);
@Autowired
    private MockMvc mockMvc;
    //用户列表查询
    @Test
    public void apiTest01()throws Exception{
        MvcResult
mvcResult=mockMvc.perform(MockMvcRequestBuilders.get("/user/list")).
                andExpect(MockMvcResultMatchers.status().isOk()).andReturn();
        log.info("响应状态:{}",mvcResult.getResponse().getStatus());
        log.info("响应内容:{}",mvcResult.getResponse().getContentAsString());;
   }
    // 用户名记录查询
    @Test
    public void apiTest02()throws Exception{
        MvcResult
mvcResult=mockMvc.perform(MockMvcRequestBuilders.get("/user/uname/admin")).
                andExpect(MockMvcResultMatchers.status().isOk()).andReturn();
        log.info("响应状态:{}",mvcResult.getResponse().getStatus());
        log.info("响应内容:{}",mvcResult.getResponse().getContentAsString());;
   }
}

```



# 全新

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.0.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.xxxx</groupId>
    <artifactId>sa-token-demo-springboot</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>sa-token-demo-springboot</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--web依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!-- commons-lang3 -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <version>3.5</version>
        </dependency>

        <!-- lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <scope>provided</scope>
        </dependency>
        <!-- jdbc 与事务包 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <!-- springboot整合mybaits包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.3</version>
        </dependency>
        <!-- mysql数据库驱动包 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version><!--$NO-MVN-MAN-VER$-->
        </dependency>
        <!-- commons-pool2 对象池依赖 -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
        </dependency>
        <!-- 热部署 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
        <!-- swagger2 依赖 -->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.7.0</version>
        </dependency>
        <!-- Swagger第三方ui依赖 -->
        <dependency>
            <groupId>com.github.xiaoymin</groupId>
            <artifactId>swagger-bootstrap-ui</artifactId>
            <version>1.9.6</version>
        </dependency>

        <!--mybatis-plus 依赖-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.3.1.tmp</version>
        </dependency>
        <!--mybatis-plus 代码生成器依赖-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-generator</artifactId>
            <version>3.3.1.tmp</version>
        </dependency>
        <!--freemarker 依赖-->
        <dependency>
            <groupId>org.freemarker</groupId>
            <artifactId>freemarker</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
        <!-- json -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.47</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```

CodeGenerator.class

```java
public class CodeGenerator {

	/**
	 * <p>
	 * 读取控制台内容
	 * </p>
	 */
	public static String scanner(String tip) {
		Scanner scanner = new Scanner(System.in);
		StringBuilder help = new StringBuilder();
		help.append("请输入" + tip + "：");
		System.out.println(help.toString());
		if (scanner.hasNext()) {
			String ipt = scanner.next();
			if (StringUtils.isNotEmpty(ipt)) {
				return ipt;
			}
		}
		throw new MybatisPlusException("请输入正确的" + tip + "！");
	}

	public static void main(String[] args) {
		// 代码生成器
		AutoGenerator mpg = new AutoGenerator();

		// 全局配置
		GlobalConfig gc = new GlobalConfig();
		String projectPath = System.getProperty("user.dir");
		gc.setOutputDir(projectPath + "/src/main/java");
		//作者
		gc.setAuthor("queening");
		//打开输出目录
		gc.setOpen(false);
		//xml开启 BaseResultMap
		gc.setBaseResultMap(true);
		//xml 开启BaseColumnList
		gc.setBaseColumnList(true);
		// 实体属性 Swagger2 注解
		gc.setSwagger2(true);
		mpg.setGlobalConfig(gc);

		// 数据源配置
		DataSourceConfig dsc = new DataSourceConfig();
		dsc.setUrl("jdbc:mysql://106.52.243.120:3306/base?useUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia" +
				"/Shanghai");
		dsc.setDriverName("com.mysql.jdbc.Driver");
		dsc.setUsername("root");
		dsc.setPassword("acdegiafec6");
		mpg.setDataSource(dsc);

		// 包配置
		PackageConfig pc = new PackageConfig();
		pc.setParent("com.xxxx.satokendemospringboot")
				.setEntity("pojo")
				.setMapper("mapper")
				.setService("service")
				.setServiceImpl("service.impl")
				.setController("controller");
		mpg.setPackageInfo(pc);

		// 自定义配置
		InjectionConfig cfg = new InjectionConfig() {
			@Override
			public void initMap() {
				// to do nothing
			}
		};

		// 如果模板引擎是 freemarker
		String templatePath = "/templates/mapper.xml.ftl";
		// 如果模板引擎是 velocity
		// String templatePath = "/templates/mapper.xml.vm";

		// 自定义输出配置
		List<FileOutConfig> focList = new ArrayList<>();
		// 自定义配置会被优先输出
		focList.add(new FileOutConfig(templatePath) {
			@Override
			public String outputFile(TableInfo tableInfo) {
				// 自定义输出文件名 ， 如果你 Entity 设置了前后缀、此处注意 xml 的名称会跟着发生变化！！
				return projectPath + "/src/main/resources/mapper/" + tableInfo.getEntityName() + "Mapper"
						+ StringPool.DOT_XML;
			}
		});
		cfg.setFileOutConfigList(focList);
		mpg.setCfg(cfg);

		// 配置模板
		TemplateConfig templateConfig = new TemplateConfig();

		templateConfig.setXml(null);
		mpg.setTemplate(templateConfig);

		// 策略配置
		StrategyConfig strategy = new StrategyConfig();
		//数据库表映射到实体的命名策略
		strategy.setNaming(NamingStrategy.underline_to_camel);
		//数据库表字段映射到实体的命名策略
		strategy.setColumnNaming(NamingStrategy.underline_to_camel);
		//lombok模型
		strategy.setEntityLombokModel(true);
		//生成 @RestController 控制器
		strategy.setRestControllerStyle(true);
		strategy.setInclude(scanner("表名，多个英文逗号分割").split(","));
		strategy.setControllerMappingHyphenStyle(true);
		//表前缀
		strategy.setTablePrefix("t_");
		mpg.setStrategy(strategy);
		mpg.setTemplateEngine(new FreemarkerTemplateEngine());
		mpg.execute();
	}
}
```

GlobalExceptionResolver.class

```java
@ControllerAdvice
public class GlobalExceptionResolver{

    /**
     * 参数异常
     * @param e
     * @return
     */
    @ExceptionHandler(value = ParamsException.class)
    @ResponseBody
    public ResInfo resolverParamsException(ParamsException e) {
        ResInfo resInfo = new ResInfo();
        resInfo.setCode(e.getCode());
        resInfo.setMsg(e.getMsg());
        return resInfo;
    }

    /**
     * validation数据校验不通过
     * @param e
     * @return
     */
    @ExceptionHandler(value = BindException.class)
    @ResponseBody
    public ResInfo resolverBindException(BindException e) {
        ResInfo resInfo = new ResInfo();
        resInfo.setCode(500);
        resInfo.setMsg(e.getBindingResult().getFieldError().getDefaultMessage());
        return resInfo;
    }

    /**
     * 未登录异常
     */
    @ExceptionHandler(value = NotLoginException.class)
    @ResponseBody
    public ResInfo resolverBindException(NotLoginException e) {
        ResInfo resInfo = new ResInfo();
        resInfo.setCode(500);
        resInfo.setMsg("尚未登陆，请登录");
        return resInfo;
    }
    /**
     * 权限不足
     */
    @ExceptionHandler(value = {NotRoleException.class,NotPermissionException.class})
    @ResponseBody
    public ResInfo resolverNotRoleException(NotRoleException e) {
        ResInfo resInfo = new ResInfo();
        resInfo.setCode(500);
        resInfo.setMsg("权限不足");
        return resInfo;
    }
}
```