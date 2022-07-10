# Spring

Spring 是一个轻量级的 Java 开发框架。Spring 的核心是控制反转(**IOC**)和面向切面编程(**AOP**)。

Spring 主要有如下优点：

1.解耦

2.支持面向切面编程

3.便于集成其他框架

## IoC

全称 Inversion of Control，意思是**控制反转**。它是 Spring 框架中的一种思想。

**控制反转就是将`对象的控制权`从程序中的代码`转移`到了 Spring 的工厂，通过 Spring 的工厂完成对象的创建以及赋值。**

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b62c0141ba744201b2a5813f73dc426a~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)

也就是说之前是我们自己 new 对象、给对象中的成员变量赋值。现在是让 Spring 来帮助我们创建对象、给成员变量赋值。





## DI

DI 全称 Dependency Injection，意思是**依赖注入**，它是 IOC 的具体实现。

依赖就是说我需要你，比如 Service 层依赖 Dao 层，注入就是**赋值**。

**依赖注入：使用 Spring 的工厂和配置文件为一个类的成员变量赋值。**



## AOP

AOP: 全称 Producer Oriented Programing，即面向切面编程。

那啥是面向切面编程？其实说白了还是 Spring 的动态代理，通过代理类为原始类增加一些 额外功能（例如打印等）。



# SpringMVC

Servlet...

# SpringBoot

