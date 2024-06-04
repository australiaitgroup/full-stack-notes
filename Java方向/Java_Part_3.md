# Java_Part_3

## Table of Content

- [Spring Boot 背景](#spring-boot-背景)
- [为什么选择 Spring Boot](#为什么选择-spring-boot)
- [开始第一个项目](#开始第一个项目)
- [对象关系映射（ORM）](#对象关系映射orm)
- [Spring Data JPA](#spring-data-jpa)
- [基本查询](#基本查询)

## Spring Boot 背景

- 从 Spring 说起，2000 年左右 Java 行业主要使用 EJB，然而 EJB 本身比较庞大复杂，企业使用起来并不便利。
- Rod Johnson 认为企业开发应该更简单，没有必要全部使用 EJB，企业开发应该是一个统一、高效的方式构造整个应用，并将单层框架以最佳组合揉合在一起，建立一个连贯的体系。
- 2002 年，Rod Johnson 编写了《Expert One-on-One J2EE Design and Development》。这本书非常经典，从书中的代码诞生了 Spring Framework。
- 随着 Spring 的不断发展，也出现了一些问题，配置文件越来越多，使用也越来越复杂，项目中常因配置错误产生问题。Spring 逐渐变得庞大复杂，背离了简洁开发的理念。随着微服务概念的兴起，Spring 开发了一个全新的技术栈：Spring Boot。

### Spring Boot 框架

Spring Boot 是由 Pivotal 团队提供的全新框架，旨在简化新 Spring 应用的初始搭建及开发过程。该框架使用特定的方式进行配置，使开发人员无需定义样板化的配置。使用 Spring Boot 可以大大简化开发模式，所有常用框架都有对应的组件支持。

官网介绍：[Spring Boot](https://spring.io/projects/spring-boot)

> Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

Spring Boot 是一套全新的框架，源于 Spring 家族，因此具备 Spring 的所有功能，而且更易使用；Spring Boot 以约定大于配置为核心思想，默认进行许多设置，大多数 Spring Boot 应用只需要很少的 Spring 配置。Spring Boot 开发了许多应用集成包，支持绝大多数开源软件，让我们以低成本集成其他主流开源软件。

#### Spring Boot 特性

- 使用 Spring 项目引导页可以在几秒内构建一个项目
- 方便对外输出各种形式的服务，如 REST API、WebSocket、Web、Streaming、Tasks
- 简洁的安全策略集成
- 支持关系数据库和非关系数据库
- 支持运行期内嵌容器，如 Tomcat、Jetty
- 强大的开发包，支持热启动
- 自动管理依赖
- 自带应用监控
- 支持各种 IDE，如 IntelliJ IDEA、NetBeans

## 为什么选择 Spring Boot

- 从软件发展的角度来看，越简单的开发模式越受欢迎。简单的开发模式释放更多生产力，让开发人员将精力集中在业务上，而不是各种配置和语法的门槛上。Spring Boot 尽可能简化应用开发的门槛。
- Spring Boot 集成的技术栈几乎都是各互联网公司在使用的技术，按照 Spring Boot 的路线学习，基本可以了解国内外互联网公司的技术特点。
- Spring Boot 和微服务架构是未来软件开发的一个大趋势，越早参与其中受益越大。

## 开始第一个项目

- 访问 [Spring Initializr](http://start.spring.io/)。
- 选择构建工具 Gradle，Spring Boot 版本 2.1.1 及一些工程基本信息，可参考下图：

### 项目目录结构

- **com.company.project** 目录下：
  - **ProjectNameApplication.java**：建议放到根目录下，是项目的启动类，Spring Boot 项目只能有一个 `main()` 方法。
  - **util/comm**：建议放置公共类，如全局配置文件、工具类等。
  - **domain/model/entity**：用于实体（Entity）与数据访问层（Repository）。
  - **repository**：数据库访问层代码。
  - **service**：业务类代码。
  - **web/controller**：页面访问控制层。
  - **factory, handler, builder** 等
- **resources** 目录下：
  - **static**：存放 Web 访问的静态资源，如 JS、CSS、图片等。
  - **templates**：存放页面模板。
  - **application.properties**：项目配置信息。
- **test** 目录：存放单元测试代码

## 对象关系映射（ORM）

- 对象关系映射（Object Relational Mapping，简称 ORM）模式用于解决面向对象与关系数据库之间的不匹配现象。简单来说，ORM 是通过使用描述对象和数据库之间映射的元数据，将程序中的对象自动持久化到关系数据库中。
- 开发一个应用程序时（不使用 O/R Mapping），可能会写很多数据访问层代码，用于从数据库保存、删除、读取对象信息等。这些代码总是重复的。ORM 提供了解决方案，简化了将程序中的对象持久化到关系数据库中的操作。
- ORM 框架的本质是简化操作数据库的编码，在 Java 领域，主要有两种框架：Hibernate 和 MyBatis。两者各有特点，在企业级系统开发中可以根据需求灵活使用。传统企业多喜欢使用 Hibernate，而互联网行业通常使用 MyBatis。
- JPA（Java Persistence API）是 Sun 官方提出的 Java 持久化规范，为 Java 开发人员提供了一种对象/关联映射工具来管理 Java 应用中的关系数据，旨在简化现有的持久化开发工作和整合 ORM 技术。JPA 在吸收现有 ORM 框架（如 Hibernate、TopLink、JDO）优点的基础上发展而来，具有易于使用、伸缩性强等优点。JPA 受到了极大的支持和赞扬，包括 Spring 与 EJB3.0 的开发团队。
- 注意：JPA 是一套规范，不是一套产品。像 Hibernate、TopLink、JDO 它们是产品，如果这些产品实现了 JPA 规范，我们就可以称它们为 JPA 的实现产品。

## Spring Data JPA

- Spring Data JPA 是 Spring 基于 ORM 框架、JPA 规范封装的一套 JPA 应用框架，使开发者用极简的代码实现对数据的访问和操作。它提供了增、删、改、查等常用功能，且易于扩展。学习并使用 Spring Data JPA 可以极大提高开发效率。
- Spring Data JPA 解放了 DAO 层的操作，几乎所有 CRUD 都可以依赖它实现。

### 添加依赖

```java
compile('org.springframework.boot:spring-boot-starter-data-jpa')
compile('mysql:mysql-connector-java')
compile('org.apache.commons:commons-lang3:3.1')
```

### 添加配置文件

```java
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver

spring.jpa.properties.hibernate.hbm2ddl.auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
spring.jpa.show-sql=true
```

- `hibernate.hbm2ddl.auto` 参数主要用于自动创建、更新或验证数据库表结构，有四个值：
  - `create`：每次加载 Hibernate 时都会删除上一次生成的表，然后根据 model 类重新生成新表，即使两次没有任何改变。这会导致数据库表数据丢失。
  - `create-drop`：每次加载 Hibernate 时根据 model 类生成表，但 sessionFactory 一关闭，表就自动删除。
  - `update`：最常用的属性，第一次加载 Hibernate 时根据 model 类自动建立表结构（前提是先建立好数据库），以后加载 Hibernate 时根据 model 类自动更新表结构，即使表结构改变，但表中的行仍然存在，不会删除以前的行。注意，部署到服务器后，表结构不会立即建立，需等待应用第一次运行后才会。
  - `validate`：每次加载 Hibernate 时，验证数据库表结构，只与数据库中的表进行比较，不会创建新表，但会插入新值。
- `dialect`：指定生成表名的存储引擎为 InnoDB。
- `show-sql`：是否打印自动生成的 SQL，方便调试时查看。

## 基本查询

- 基本查询分为两种：一种是 Spring Data 默认实现的，一种是根据查询方法自动解析成 SQL。

### 复杂查询

- 实际开发中需要分页、筛选、连表等查询时，需要特殊方法或自定义 SQL。

### 自定义 SQL 查询

- Spring Data 可以根据方法名定义的方式实现大部分 SQL 查询，但如果需要使用自定义 SQL，Spring Data 也支持。在查询方法上使用 `@Query` 注解，如

涉及到删除和修改需要加上 `@Modifying`。也可以根据需要添加 `@Transactional` 支持事务管理，查询超时设置等。

### 多表查询

- 在 Spring Data JPA 中，多表查询有两种实现方式：
  - 使用 Hibernate 的级联查询
  - 创建一个结果集接口来接收连表查询结果

特别注意，这里的 SQL 是 HQL，需要写类的名称和属性。

### 其他

- 使用枚举时，如果选择数据库中存储的是枚举对应的 String 类型，而不是枚举的索引值，需要在属性上添加 `@Enumerated(EnumType.STRING)` 注解：

```java
@Enumerated(EnumType.STRING)
@Column(nullable = true)
private UserStatus status;
```
