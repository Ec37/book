# 一 Spring Cloud 常用的注解

## @SpringBootApplication是SpringBoot启动类，包含三个注解，他们的作用分别是：

> @Configuration：表示这个类中定义了bean，会把这个类中bean加载到spring容器中

> @ComponentScan：表示程序启动时自动扫描当前包及子包下所有类，如果不设置basePackage的话，默认会扫描包的所有类，所以最好加上basePackage(@ComponentScan({"..."}))

> @EnableAutoConfiguration：表示会在你开启某些功能的时候自动配置，这个注解告诉Spring Boot 根据添加的jar包依赖猜测你想要如何配置Spring。由于spring-boot-starter-web添加了Tomcat和Spring MVC ，所以auto-configuration将假定你正在开发web应用，并对Spring进行相应的配置

## @EnableDiscoveryClient和@EnableEurekaClient

> @EnableDiscoveryClient基于spring-cloud-commons，@EnableEurekaClient基于spring-cloud-netfix,如果选用eureka作为注册中心，那么推荐使用@EnableEurekaClient，如果选择其他注册中心，那么推荐使用@EnableDiscoveryClient。

## @Mapper 和 @MapperScan

这是MyBatis的注解

> Mapper类上面添加注解@Mapper，这种方式要求每一个Mapper都要添加此注解
> 使用@MapperScan可以指定要扫描的Mapper类的包路径:
> @MapperScan("com.demo.\*.mapper")
> @MapperScan("com.test.\*.mapper","com.demo.\*.mapper")

## @EnableTransactionManagement 和 @Transactional

@EnableTransactionManagement放在@SpringBootApplication附近即可

>Spring Boot 使用事务非常简单，首先使用注解@EnableTransactionManagement（启动注解事务管理，等同于xml配置的<tx:annotation-driven />开启事务支持，然后在访问数据库的Service方法上添加@Transactional即可

## @Bean 和 @Configuration

> @Bean标记在方法上（返回某个实例的方法），等价于spring的xml配置文件中的<bean>
> 作用：注册bean对象

> @Configuration标记在类上，相当于把该类作为spring的xml配置文件中的<beans>
> 作用：配置spring容器（应用上下文）


## @GetMapping 和 @PostMapping

> Spring4.3引进了(@GetMapping、@PostMapping、@PutMapping、@DeleteMapping、@PatchMapping)，用于简化常用的HTTP方法的映射，并更好的表达注解方法的语义。

> @GetMapping是一个组合注解，是@RequestMapping(method=RequestMethod.GET)的缩写。
> @PostMapping是一个组合注解，是@RequestMapping(method=RequestMethod.POST)的缩写。

## @LoadBalanced

> Spring Cloud的commons模块提供了一个@LoadBalanced注解，方便我们对RestTemplate添加一个LoadBalancedClient，以实现客户端负载均衡，通过源码发现这是一个标记注解，我们可以通过ribbon实现客户端的负载均衡功能

## @PropertySource 和 @ImportResource

使用注解加载外部的配置文件

> 加载properties文件：
> @PropertySource(value={"classpath:spring-demo.properties"})

> 加载xml文件：
> @ImportResource(locations={"classpath:spring-demo.xml"})

## @Value

> 举个例子：
> application.properties有这些内容：
>> member.id=001
member.name=张三

> 那样在Java中可以用注解这样子取：
>> @Value("member.id")
private String memberId;

# 二、 Eureka实现原理

Eureka服务治理基础架构三个核心要素。

## 1. 服务注册中心

Eureka分为服务端和客户端，Eureka服务端提供服务注册与发现的功能。

## 2. 服务提供者

提供服务的应用，Spring Boot 应用或者遵循Eureka通信机制的的应用。
应用将自己注册到Eureka注册中心，以供其他应用的发现。

## 3. 服务消费者

消费者从服务注册中心获取服务列表，通过客户端负载均衡某种算法轮询服务列表。
然后调用其所需要的服务，也即是调用对应的服务提供者。

ps：在某些情况下，服务既是提供者，也是消费者。
比如服务A调用服务B，服务B调用服务C，这样服务B就是既是提供者，也是消费者

# 三、 服务治理机制

