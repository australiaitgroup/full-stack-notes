# Java_Part_4

## Table of Content

- [Spring IOC 和 AOP](#spring-ioc-和-aop)
  - [什么是控制反转（IoC）？](#什么是控制反转ioc)
  - [什么是依赖注入（DI）？](#什么是依赖注入di)
  - [Spring 开发策略](#spring-开发策略)
  - [IoC](#ioc)
  - [Spring IoC 容器](#spring-ioc-容器)
  - [通过扫描装配 Bean](#通过扫描装配-bean)
  - [基于 Setter 的依赖注入](#基于-setter-的依赖注入)
  - [基于字段的依赖注入](#基于字段的依赖注入)
  - [@Autowired 注解](#autowired-注解)
  - [带有参数的构造方法的装配](#带有参数的构造方法的装配)
  - [Bean 的生命周期](#bean-的生命周期)
  - [使用属性文件](#使用属性文件)
  - [使用 @Profile 指定不同环境](#使用-profile-指定不同环境)
- [AOP](#aop)

## Spring IOC 和 AOP

### 什么是控制反转（IoC）？

控制反转（Inversion of Control, IoC）是一种软件工程中的原则，通过它框架可以控制程序的流程，并调用我们的自定义代码。为了实现这一点，框架使用内置了额外行为的抽象。如果我们想要添加自己的行为，需要扩展框架的类或插入自己的类。

- 这种架构的优点：
  - 解耦任务的执行和其实现
  - 更容易在不同实现之间切换
  - 提高程序的模块化
  - 通过隔离组件或模拟其依赖项，使测试程序更容易

IoC 主要的作用就是解耦各个组件，让高层模块不依赖底层模块，而是通过接口和抽象实现。IoC 的核心思想在于，资源不由使用资源的双方管理，而由第三方管理，这带来了许多好处：

1. 资源集中管理，实现资源的可配置和易管理。
2. 降低使用资源双方的依赖程度，即耦合度。

### 什么是依赖注入（DI）？

依赖注入（Dependency Injection, DI）是一种实现 IoC 的模式，其中被反转的控制是对象依赖关系的设置。对象与其他对象的连接，或将对象“注入”到其他对象，是由装配器完成的，而不是由对象自己完成的。

- DI 和 IoC 一起工作
- DI 的缺点：管理依赖关系不方便。如果我们想要为 MyClass2 添加另一个依赖项，需要自己更改代码。

```java
public class Main {
  public static void main(String[] args) {
    MyClass4 myClass4 = new MyClass4();
    MyClass3 myClass3 = new MyClass3();
    MyClass2 myClass2 = new MyClass2(myClass3, myClass4);
    MyClass1 myClass1 = new MyClass1(myClass2);
    myClass1.doSomething();
  }
}
```

### DI 和 IoC 一起工作

使用 IoC，依赖关系由容器管理，程序员无需承担这一负担。使用 @Autowired 注解，容器会在需要时注入依赖项，程序员无需自己创建或管理这些依赖项。

```java
public class MyClass2 {
  @Autowired
  private MyClass3 myClass3;
  @Autowired
  private MyClass4 myClass4;
  public void doSomething() {
    myClass3.doSomething();
    myClass4.doSomething();
  }
}
```

## Spring 开发策略

Spring 最根本的使命是简化 Java 开发。为了降低 Java 开发的复杂性，Spring 采取以下四种关键策略：

- 基于 POJO 的轻量级和最小侵入性编程
- 通过依赖注入和面向接口实现松耦合
- 基于切面和惯例进行声明式编程
- 通过切面和模板减少样板代码

### IoC

控制反转（Inversion of Control, IoC）是 Spring 的核心思想，贯穿始终。对于 Spring 框架来说，IoC 意味着由 Spring 来负责控制对象的生命周期和对象间的关系。所有的类都会在 Spring 容器中登记，告诉 Spring 你是什么，你需要什么，然后 Spring 会在系统运行到适当的时候，把你需要的东西主动给你，同时也把你交给其他需要你的东西。所有类的创建、销毁都由 Spring 控制，控制对象生命周期的不再是引用它的对象，而是 Spring。

IoC 容器需要具备两个基本功能：

- 通过描述管理 Bean，包括发布和获取 Bean；
- 通过描述完成 Bean 之间的依赖关系。

### Spring IoC 容器

在 Spring 中，IoC 容器管理的对象称为 Bean，这与 JavaBean 并没有关系。

- **BeanFactory**：所有的 IoC 容器都需要实现的顶级容器接口。Bean 工厂借助配置文件实现对 JavaBean 的配置和管理，用于向使用者提供 Bean 的实例。
- **ApplicationContext**：构建在 BeanFactory 之上，提供了更多实用功能。在现实中，我们使用的大部分 Spring IoC 容器是 ApplicationContext 接口的实现类。

### 通过扫描装配 Bean

- 使用注解 @Bean 将一个个 Bean 注入 Spring IoC 容器中非常繁琐。Spring 允许通过扫描装配 Bean 到 IoC 容器中，使用的注解是 @Component 和 @ComponentScan。@Component 标明哪个类被扫描进入 Spring IoC 容器，而 @ComponentScan 则标明采用何种策略去扫描装配 Bean。

### 基于 Setter 的依赖注入

对于基于 Setter 的依赖注入，容器会在调用无参构造函数或无参静态工厂方法实例化 Bean 后，调用类的 Setter 方法。让我们使用注解来创建这个配置：

构造器注入和 Setter 注入可以结合使用。Spring 文档推荐对强制依赖项使用构造器注入，对可选依赖项使用 Setter 注入。

### 基于字段的依赖注入

我们可以通过 @Autowired 注解标记依赖项来注入它们：

```java
public class Store {
  @Autowired
  private Item item;
}
```

在构建 Store 对象时，如果没有构造函数或 Setter 方法注入 Item Bean，容器会使用反射将 Item 注入 Store。这种方法看起来更简单和清洁，但不推荐使用，因为它有一些缺点：

- 使用反射注入依赖项比构造器注入或 Setter 注入成本更高。
- 使用这种方法很容易不断添加多个依赖项。如果使用构造器注入，多个参数会让我们意识到这个类做了不止一件事，可能违反了单一职责原则。

### @Autowired 注解

@Autowired 的默认规则：首先根据类型找到对应的 Bean，如果对应类型的 Bean 不是唯一的，会根据其属性名称和 Bean 的名称进行匹配。如果匹配成功，就会使用该 Bean；如果仍无法匹配，就会抛出异常。

- 消除歧义性——@Primary 和 @Qualifier
- @Primary 的含义是告诉 Spring IoC 容器，当发现有多个同样类型的 Bean 时，请优先使用这个进行注入。
- @Qualifier 的配置项 value 需要一个字符串，与 @Autowired 组合，通过类型和名称一起找到 Bean。

### 带有参数的构造方法的装配

使用 @Autowired 注解对构造方法的参数进行注入：

```java
@Component
public class BusinessPerson implements Person {
  private Animal animal = null;

  public BusinessPerson(@Autowired @Qualifier("dog") Animal animal) {
    this.animal = animal;
  }

  @Override
  public void service() {
    this.animal.use();
  }

  @Override
  public void setAnimal(Animal animal) {
    this.animal = animal;
  }
}
```

### Bean 的生命周期

Spring IoC 初始化和销毁 Bean 的过程，就是 Bean 的生命周期。主要分为 Bean 定义、Bean 的初始化、Bean 的生命周期和 Bean 的销毁四个部分。

- Bean 定义过程：
  - Spring 通过配置（如 @ComponentScan 定义的扫描路径）找到带有 @Component 的类，这是一个资源定位的过程。
  - 一旦找到资源，就开始解析，并将定义信息保存起来。注意，此时还没有初始化 Bean，也没有 Bean 的实例，只有 Bean 的定义。
  - 然后将定义发布到容器中。此时，IoC 容器只有 Bean 的定义，没有 Bean 的实例。

### Bean 的初始化流程

@ComponentScan 中还有一个配置项 lazyInit，只接受 Boolean 值，默认值为 false，即默认不进行延迟初始化。因此，Spring 会对 Bean 进行实例化和依赖注入。

### 使用属性文件

在 Spring Boot 中使用属性文件

，可以采用默认的 application.properties，也可以使用自定义配置文件。

```java
compileOnly "org.springframework.boot:spring-boot-configuration-processor"
@Value("${database.driverName}")
@ConfigurationProperties("database")
```

### 使用 @Profile 指定不同环境

启动时选择选项 -Dspring.profiles.active 配置的值为 {profile}，则会使用 application-{profile}.properties 文件代替默认的 application.properties 文件，通过这样可以有效地切换各类环境，如开发、测试和生产。

```bash
JAVA_OPTS="-Dspring.profiles.active=dev"
```

## AOP

面向切面编程（Aspect Oriented Programming, AOP）

AOP 是面向对象编程的有益补充。AOP 将与业务无关但为业务模块所共同调用的逻辑或责任进行封装。应用 AOP 的功能举例：

- Authentication 权限
- Caching 缓存
- Context passing 内容传递
- Error handling 错误处理
- Lazy loading 懒加载
- Debugging 调试
