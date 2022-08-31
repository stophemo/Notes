# SpringBoot



整合其他框架

SpringCloud 的基础

## 快速入门



### @RestController

- 并非SpringBoot提供，而是SpringMVC提供的注解。

- 如果在类上加上`@RestController`, 该类中所有SpringMVCUrl接口映射都是返回json格式

- 在每个方法上加上了`@ResponseBody`注解，返回json格式



微服务接口开发 Rest风格 数据传输格式 json格式 协议 http协议



#### @RequestMapping

跳转



## 

### @EnableAutoConfigration

启动类 注解

```java
public static void main (String[] args) {
    SpringApplication.run(启动类.class, args);
}
```

#### @ComponentScan

@ComponentScan("包名")

SpringMVC提供

指定注解扫描范围 或者说将包下所有类注入到IOC容器里面去



**SpringBoot：**

### SpringBoot：@SpringBootAPPlication

封装了以下注解

@SpringBootApplication

@EnableAutoconfigration

@ComponentScan

（扫描App类同级及子包）

单独建个启动类

```java
@SpringBootAPPlication
public class App {
   public static void main (String[] args) {
       SpringApplication.run(App.class);
   }
}
```



## Web开发

YML与Properties用法

application.properties：

```xml
mayikt.name=mayikt
mayikt.age=22
```

application.yml:

```yml
mayikt:
	name: mayikt
	age: 22
```





## JDBCTemplate



## Lombok

安装插件 + 引入依赖



### @Data

### @Slf4j

```java
private static Logger log = Logger.getLogger(UserEntity.class)
```

