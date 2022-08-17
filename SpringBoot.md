# 基础部分

### 1 引言

#### 1.1 概述

SpringBoot提供了一种快速使用Spring的方式，基于约定优于配置的思想，可以让开发人员不必在配置与逻辑业务之间进行思维的切换，全身心的投入到逻辑业务的代码编写中，从而大大提高了开发的效率，一定程度上缩短了项目周期。 2014 年 4 月，Spring Boot 1.0.0 发布。Spring的顶级项目之一(https://spring.io)。

#### 1.2 Spring 缺点

- 配置繁琐

虽然Spring的组件代码是轻量级的，但它的配置却是重量级的。一开始，Spring用XML配置，而且是很多XML配置。Spring 2.5引入了基于注解的组件扫描，这消除了大量针对应用程序自身组件的显式XML配置。Spring 3.0引入了基于Java的配置，这是一种类型安全的可重构配置方式，可以代替XML。所有这些配置都代表了开发时的损耗。因为在思考Spring特性配置和解决业务问题之间需要进行思维切换，所以编写配置挤占了编写应用程序逻辑的时间。和所有框架一样，Spring实用，但它要求的回报也不少。

- 依赖繁琐


项目的依赖管理也是一件耗时耗力的事情。在环境搭建时，需要分析要导入哪些库的坐标，而且还需要分析导入与之有依赖关系的其他库的坐标，一旦选错了依赖的版本，随之而来的不兼容问题就会严重阻碍项目的开发进度

#### 1.3 SpringBoot功能

- 自动配置

Spring Boot的自动配置是一个运行时（更准确地说，是应用程序启动时）的过程，考虑了众多因素，才决定Spring配置应该用哪个，不该用哪个。该过程是SpringBoot自动完成的。

- 起步依赖


起步依赖本质上是一个Maven项目对象模型（Project Object Model，POM），定义了对其他库的传递依赖，这些东西加在一起即支持某项功能。简单的说，起步依赖就是将具备某种功能的坐标打包到一起，并提供一些默认的功能。

- 辅助功能


提供了一些大型项目中常见的非功能性特性，如嵌入式服务器、安全、指标，健康检测、外部配置等。

#### 1.4 总结

Spring Boot 并不是对 Spring 功能上的增强，而是提供了一种快速使用 Spring 的方式

- Spring缺点：
  - 配置繁琐
  - 依赖繁琐
- SpringBoot功能：
  - 自动配置
  - 起步依赖（依赖传递）
  - 依赖繁琐



### 2  快速入门

#### 2.1 需求

搭建SpringBoot工程，定义HelloController.hello()方法，返回”Hello SpringBoot!”。

#### 2.2 [Maven构建实现步骤](https://spring.io/guides/gs/maven/)

1）创建Maven项目

​	直接创建即可，不需要选择什么。

2）导入SpringBoot起步依赖

​	pom.xml文件导入如下依赖

```xml
<!--SpringBoot工程需要继承的父工程-->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.5.4</version>
</parent>

<dependencies>
    <!--web开发的起步依赖-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

3）定义Controller

```java
package com.itheima.controller;

@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String hello() {
        return "Hello SpringBoot!";
    }
}
```

4）编写引导类

```java
package com.itheima;

/**
 * 引导类。SpringBoot项目的入口
 */
@SpringBootApplication
public class HelloApplication {
    public static void main(String[] args) {
        SpringApplication.run(HelloApplication.class, args);
    }
}

```

5）启动测试
	直接运行main方法即可

<img src="https://img-blog.csdnimg.cn/06d026ecd30143d7b1cefece009edf5c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16" alt="在这里插入图片描述" style="zoom:50%;" />

6）总结

- SpringBoot在创建项目时，使用jar的打包方式。
- SpringBoot的引导类，是项目入口，运行main方法就可以启动项目

### 3 SpringBoot起步依赖原理分析

在spring-boot-starter-parent中定义了各种技术的版本信息，组合了一套最优搭配的技术版本。
在各种starter中，定义了完成该功能需要的坐标合集，其中大部分版本信息来自于父工程。
我们的工程继承parent，引入starter后，通过依赖传递，就可以简单方便获得需要的jar包，并且不会存在版本冲突等问题

### 4 配置

SpringBoot是基于约定的，所以很多配置都有默认值，但如果想使用自己的配置替换默认配置的话，就可以使用 **application.properties**或者**application.yml(application.yaml)**进行配置。

```properties
properties：
server.port=8080
```

```yml
server:
	port: 8080
```

- SringBoot提供了2种配置文件类型：properteis和yml/yaml
- 默认配置文件名称：application
- 在同一级目录下优先级为：properties > yml > yaml

#### 4.1 yaml

yaml：YAML全称是 YAML Ain’t Markup Language 。YAML是一种直观的能够被电脑识别的的数据数据序列化格式，并且容易被人类阅读，容易和脚本语言交互的，可以被支持YAML库的不同的编程语言程序导入，比如： C/C++, Ruby, Python, Java, Perl, C#, PHP等。YML文件是以数据为核心的，比传统的xml方式更加简洁。 YAML文件的扩展名可以使用.yml或者.yaml。
对比：

- properties：


```properties
server.port=8080
server.address=127.0.0.1
```

- xml：


```xml
<server>
    <port>8080</port>

    <address>127.0.0.1</address>

</server>
```

- yaml：

```yaml
server: 
    port: 8080
    address: 127.0.0.1
name: abc
```

##### 4.1.1 yaml基本语法

- 大小写敏感
- 数据值前边必须有空格，作为分隔符
- 使用缩进表示层级关系
- 缩进时不允许使用Tab键，只允许使用空格（各个系统 Tab对应的 空格数目可能不同，导致层次混乱）。
- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
- `#`表示注释，从这个字符一直到行尾，都会被解析器忽略。

##### 4.1.2 yaml数据格式

- 对象（map）：键值对的集合

```yaml
person:
	name:zhangsan
	
#行内写法
person: {name: zhangsan}
```

- 数组：一组按次序排列的值

```yaml
address:
- beijing
- shanghai

#行内写法
address: [beijing,shanghai]
```

- 纯量：可以理解成常量，单个的，不可再分的值

```yaml
msg1: 'hello \n world' # 单引忽略转义字符
msg2: "hello \n world" # 双引识别转义字符
```

- yaml参数引用

```yaml
name: lisi
person:	
	name :${name} #引用上边定义的name值
```

#### 4.2 读取配置内容

##### 4.2.1 @Value

```java
@Value("${name}")
private String name;
@Value("${person.name}")
private String name1;
@Value(("${address[0]}"))
private String address1;
@Value("${msg1}")
private String msg1;
@Value("${msg2}")
private String msg2;

@RequestMapping("/hello2")
public String hello2(){
    System.out.println(name);
    System.out.println(name1);
    System.out.println(address1);
    System.out.println(msg1);
    System.out.println(msg2);
    return "Hello SpringBoot !";
}
```

输出结果：
xpp
xpp
beijing
hello \n springboot
hello 
springboot

##### 4.2.2 Environment

```java
@Autowired
private Environment env;

@RequestMapping("/hello2")
public String hello2(){
    System.out.println(env.getProperty("name"));
    System.out.println(env.getProperty("person.age"));
    System.out.println(env.getProperty("address[0]"));

    return "Hello SpringBoot !";
}
```

输出：
xpp
23
beijing

##### 4.2.3 @ConfigurationProperties

```j
@Component//表示这个类被spring识别了
@ConfigurationProperties(prefix = "person")//绑定前缀
//下面四个注解为LomBok提供的，简化开发，自动帮我们写好get，set，有参，无参和toString方法
@Data
@NoArgsConstructor
@AllArgsConstructor
@ToString
public class Person {
    private String name;
    private Integer age;
    private String[] address;
}
```

```java
@Autowired
private Person person;

@RequestMapping("/hello2")
public String hello2(){
    System.out.println(person);
    return "Hello SpringBoot !";
}
```

输出结果：
Person(name=xpp, age=23, address=[benjing, shanghai])

### 5 profile

我们在开发Spring Boot应用时，通常同一套程序会被安装到不同环境，比如：开发、测试、生产等。其中数据库地址、服务器端口等等配置都不同，如果每次打包时，都要修改配置文件，那么非常麻烦。**profile功能就是来进行动态配置切换的。**

#### 5.1 profile配置方式

1. 多profile文件方式

提供多个配置文件，每一个代表一种环境：

- application-dev.properties/yml 开发环境
- application-test.properties/yml 测试环境
- application-pro.properties/yml 生产环境

注意！：格式必须为application-xxx.properties/yml

<img src="https://img-blog.csdnimg.cn/86a90062ddbf479b8766de400b7c84d8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16" alt="在这里插入图片描述" style="zoom:50%;" />

在主配置文件`application.properties`选择用哪种环境：

**格式**：`spring.profiles.active=xxx`

```yaml
spring.profiles.active=dev
```

2. yaml多文档方式

`---`用来划分yaml文件区域

```yaml
---

server:
  port: 8081
spring:
  config:
    activate:
      on-profile: dev
---
server:
  port: 8082
spring:
  config:
    activate:
      on-profile: test
---
server:
  port: 8083
spring:
  config:
    activate:
      on-profile: pro
---
spring:
  profiles:
    active: test

```

#### 5.2 profile激活方式

1. 配置文件

   即上面所讲的：在配置文件中配置：`spring.profiles.active=dev`

2. 虚拟机

   在`VM options` 指定：`-Dspring.profiles.active=xxx`

   <img src="https://img-blog.csdnimg.cn/3d68346de8ba4a1fb8a555ec6f49252f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16" alt="在这里插入图片描述" style="zoom:50%;" />

3. 命令行参数

   java –jar xxx.jar --spring.profiles.active=xxx

   ①直接在`Program arguments`配置

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/899f44a2a6db49d581fb1b2198f98866.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16)

②打包方式配置

![在这里插入图片描述](https://img-blog.csdnimg.cn/b03a19d6f0504cbe93ca4983c4003d9f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16)

进入target文件夹（快捷键`Ctrl+Alt+F12`)

![在这里插入图片描述](https://img-blog.csdnimg.cn/03842cbcf18b4ab1a0ef1c9d777d9f14.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16)

在当前目录打开cmd

![在这里插入图片描述](https://img-blog.csdnimg.cn/6ca0eacfa2a54fdd9eb9527aa0df3ab4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16)

输入`java –jar xxx.jar`启动SpringBoot项目

![在这里插入图片描述](https://img-blog.csdnimg.cn/59f0fde462024941a30644df097d59a6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16)

输入`java –jar xxx.jar --spring.profiles.active=xxx`即可更改环境

![在这里插入图片描述](https://img-blog.csdnimg.cn/d4d860e7b6254f4a9e30415e32d5cc18.png)

### 6 内置配置加载顺序

Springboot程序启动时，会从以下位置加载配置文件：

1. file:./config/：当前项目下的/config目录下
2. file:./ ：当前项目的根目录
3. classpath:/config/：classpath的/config目录
4. classpath:/ ：classpath的根目录（之前我们用的就是这种）

加载顺序为上文的排列顺序，高优先级配置的属性会生效

<img src="https://img-blog.csdnimg.cn/4fd36e80251645d1877370a44394907f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATEwuTEVCUk9O,size_20,color_FFFFFF,t_70,g_se,x_16" alt="在这里插入图片描述" style="zoom:33%;" />

### 7 外部配置加载顺序

通过[官网](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html)查看外部属性加载顺序

### 8 SpringBoot整合其他框架

https://blog.csdn.net/qq_45966440/article/details/120450596?spm=1001.2014.3001.5502

#### 8.1 整合Junit

#### 8.2 整合redis

#### 8.3 整合mybatis

