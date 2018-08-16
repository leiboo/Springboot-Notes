# Spring-boot 学习笔记

## （一）@Controller和@RestController的区别

相同点：都是用来表示Spring某个类的是否可以接收HTTP请求

不同点：@Controller标识一个Spring类是Spring MVC controller处理器

　　　　@RestController：@RestController是@Controller和@ResponseBody的结合体，两个标注合并起来的作用。

```java
@Controller  
@ResponseBody  
public class MyController { }  
  
@RestController  
public class MyController { } 
```

## （二） @EnableAutoConfiguration和@SpringbootApplication区别

1. @EnableAutoConfiguration这个注释告诉SpringBoot“猜”你将如何想配置Spring,基于你已经添加jar依赖项。如果spring-boot-starter-web已经添加Tomcat和Spring MVC,这个注释自动将假设您正在开发一个web应用程序并添加相应的spring设置。

　　自动配置被设计用来和“Starters”一起更好的工作,但这两个概念并不直接相关。您可以自由挑选starter依赖项以外的jar包，springboot仍将尽力自动配置您的应用程序。

spring通常建议我们将main方法所在的类放到一个root包下，@EnableAutoConfiguration（开启自动配置）注解通常都放到main所在类的上面，下面是一个典型的结构布局：

```java
com
 +- example
     +- myproject
         +- Application.java
         |
         +- domain
         |   +- Customer.java
         |   +- CustomerRepository.java
         |
         +- service
         |   +- CustomerService.java
         |
         +- web
             +- CustomerController.java
```

这样@EnableAutoConfiguration可以从逐层的往下搜索各个加注解的类，例如，你正在编写一个JPA程序（如果你的pom里进行了配置的话），spring会自动去搜索加了@Entity注解的类，并进行调用。

2. @SpringbootApplication使用@SpringbootApplication注解  可以解决根类或者配置类（我自己的说法，就是main所在类）头上注解过多的问题，一个@SpringbootApplication相当于@Configuration,@EnableAutoConfiguration和 @ComponentScan 并具有他们的默认属性值。

```java
package com.example.myproject;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication //等同于 @Configuration @EnableAutoConfiguration @ComponentScanpublic
class Application {   
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
}
```

