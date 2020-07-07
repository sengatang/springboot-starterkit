<h1 align="center">
  <br>
  <a><img src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/spring-framework.png" alt="spring boot"></a>
  <br>
  Spring Boot Starterkit
  <br>
</h1>

<h4 align="center">Production ready starterkit for Spring Boot applications.</h4>

<p align="center">
    <a alt="Java">
        <img src="https://img.shields.io/badge/Java-v1.8-orange.svg" />
    </a>
    <a alt="Spring Boot">
        <img src="https://img.shields.io/badge/Spring%20Boot-v2.1.3-brightgreen.svg" />
    </a>
    <a alt="Bootstrap">
        <img src="https://img.shields.io/badge/Bootstrap-v4.0.0-yellowgreen.svg">
    </a>
    <a alt="Material">
        <img src="https://img.shields.io/badge/Material%20Design-UI-orange.svg">  
    </a>      
    <a alt="Docker">
        <img src="https://img.shields.io/badge/Docker-v18-yellowgreen.svg" />
    </a>
    <a alt="Dependencies">
        <img src="https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen.svg" />
    </a>
    <a alt="Contributions">
        <img src="https://img.shields.io/badge/contributions-welcome-orange.svg" />
    </a>
    <a alt="License">
        <img src="https://img.shields.io/badge/license-MIT-blue.svg" />
    </a>
</p>

## Table of Contents ##
1. [Philosophy](#Philosophy)
2. [Spring Boot](#Spring-Boot)
3. [Application](#Application)
4. [Database Schema](#Database-Schema)
5. [Technology](#Technology)
6. [Application Structure](#Application-Structure)
7. [Run Locally](#Running-the-server-locally)
8. [Run Insider Docker](#Running-the-server-in-Docker-Container)
9. [API Documentation](#API-Documentation)
10. [User Interface](#User-Interface)
11. [Contributor](#Contributor)
12. [License](#License)

## Philosophy 思想 ##
Spring boot 为了减少负责性与依赖性花了很大的力气，如果你的代码是在 Spring 的生态中并且想要转向微服务，Spring boot 是一个非常好的选择。它允许轻松设置独立的基于 Spring 的应用程序，是简单快速地建立与部署微服务的理想选择。由于 hibernate 映射使用了更少的boilerplate 代码，它还可以减少数据访问的痛苦。你可以从很简单的代码入手，因为它对 Spring 平台和第三方库持一种“固执己见”的观点。 绝大部分的 Spring Boot 的应用只需要很少的 Spring 的设置。

Spring Boot 最迷人的地方在用很短的时间就可以跑起一个 server，你不需要安装像 JBoss, Websphere, Tomcat 之类的东西。你只需要把需要的库、注解配置好就可以起飞了。如果你有很多个 Spring Boot 的项目，我强烈推荐使用 IntelliJ IDEA IDE，它有很好的管理 Boot 项目的功能。你可以在 Maven 或者 Gradle 中选择一个来管理依赖。这个 starter kit 使用的是（我更熟悉的）Maven。


## Spring Boot ##
_Spring Boot 使得创建独立的，生产级别的，基于 Spring 的应用非常简单。因为它对 Spring 平台和第三方库持一种“固执己见”的观点，绝大部分的 Spring Boot 的应用只需要很少的 Spring 的设置_

**Spring Boot 是 “固执己见的(opinionated)”** : “固执己见”在这里指的是 Spring Boot 有自己的设置，项目结构，依赖，服务以及其他一些环境配置。 例如，绝大数的 Java-based web applications 使用 tomcat Server。但是当使用 Boot 的时候你不用另外任何的 Server，因为 Boot 自己有一个内嵌的 tomcat 容器。

**Spring Boot 是 “独立的(stand-alone)”** : 指的是你不需要在开发或者部署 server 的过程中再用第三方的库，它就像一个全家桶。

**Spring Boot 是 “生产级别的(production-grade)”** : 意味着使用 Spring Boot 默认开发的应用程序能够处理生产环境的所有复杂性和需求.

**Spring Boot 依然 “高度可自定义化(customizable)”** :用一个非常僵硬的，不能根据自己业务需求定制或更改的框架是非常不值当的。虽然 Boot 是“固执己见的”，你依旧可以非常简单地对它进行改变来迎合你自己的需求。




## Application 应用 ##
这个 starter kit 主要关注如何按照 Spring Framework 5.0 推荐的所有最佳实践来使用 Spring Boot，确保代码是松耦合的，应用程序中的所有层彼此完全独立，并且使用中性对象进行对话。写这个 kit 的时候我做了多关于**代码结构**和**设计模式**的研究来使这个 kit 可以成为你编写你的 web application 的很好的一个起点。



如果没有一个实现一个具体的东西的话，这个 kit 就不完整了，所以我仔细对***汽车预定系统***做了案例研究并尝试实现一个后台管理系统。它可以经由浏览器和移动应用程序，通过一系列 REST 接口与系统进行交互。这个系统有两个重要的角色：

1. 管理员
2. 普通端用户



*管理员*可以有下述一些操作：

1. 注册
2. 登陆 (Spring sessions)
3. 更新资料
4. 创建一个汽车中介
5. 往汽车中介里添加汽车
6. 添加包含预定义站点和公共汽车的行程



*端用户*可以有下述操作

1. 注册
2. 登陆 (获取 JWT token) 
3. 列出所有可用站点
4. 查询两个站点之间的行程
5. 通过时间筛选上述搜索结果
6. 预定一个行程的票



管理员接口和 REST API 有各自独立的身份验证机制。web application 使用*基于 cookie 的身份验证*（由Spring security默认提供），REST API 使用 *JWT 身份验证* 进行访问。此应用程序假定在运行服务器的本地主机上安装 “MongoDB”，或使用 docker-compose 启动 MongoDB 容器并在 docker 内将应用程序与其链接。

管理员在网站上所做的任何更改操作都会影响端用户的搜索结果，在这里你可能会发现缺少某些用例，希望你可以理解这个项目的主要目的是展现如何在 Spring Boot 中创建一个应用程序，而不是构建一个功能齐全的预订系统。

管理用户 UI 是用 Bootstrap v4 写的，能够响应各种设备。前端引擎是 Thymeleaf，因为该库具有极强的可扩展性，其自然的模板功能确保模板可以在没有后端的情况下进行原型化，这使得开发与其他流行的引擎（如JSP）相比非常快。



## Database Schema 数据库 ##
现在的数据库设计是这样的：

<img src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/db-schema.png" alt="spring boot"></a>

-  authentication 和 authorization 由 _User_ 和 _Role_ collection控制.
-  _Agency_ collection 存储汽车中介的信息与所有者
- _Stop_ collection 存储系统中所有的站点
- _Bus_ collection 存储系统中所有的汽车，核载人数，生产年限和所属中介
- _Trip_ 和 _TripSchedule_ collection 存储行程的始发站，终点站，行程时间日期，所售出车票与所剩余座位信息
- _Ticket_ collection 存储着所发售车票的所有信息



## Technology 技术 ##
这个 starter kit 用到了以下的库:

- **Spring Boot** - 后端服务器框架
- **Docker** - Containerizing 框架
- **MongoDB** - NoSQL 数据库
- **Swagger** - API 文档
- **Thymeleaf** - 框架引擎
- **Material** - UI 主题
- **Bootstrap** - CSS 框架
- **JWT** - REST API 的身份认证机制




## Application Structure 应用结构 ##
Spring Boot 是一个 “固执己见” 的框架，它使我们的生活变得非常简单，因为我们不必根据 Spring 框架的版本来选择不同的依赖的版本，所有这些都由 Spring Boot 负责。在创构建目结构时，我试图遵循相同的思想，一开始它可能看起来很复杂不知从何下手，但请相信我，一旦你开始写代码，这个结构将极大地帮助你节省在*已经得到回答的问题*上思考的时间。项目结构如下：

<img src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/project-structure.png" alt="project structure"></a>

**_Models & DTOs_**

应用程序的各种 model 在 ***model*** package 中，**DTO** (data transfer objects) 在 ***dto*** package 中。是否应该使用 DTO 是一件有争议的事情，我认为是要使用的，如果不用 DTO 的话会使得 model 和 UI 耦合非常紧密，这是任何企业项目都不想这样。DTO 使得我们可以只把前端需要的数据传给他们，而不是传整个 model，这个 model 可能由和其他 sub objects 聚合并持久化在数据库中（即模型非常复杂）。模型到 DTO 的映射可以使用 ModelMapper utility 来处理，但是只有当 DTO 与相关模型几乎相似时才有用，而事实并非总是如此，因此我更喜欢使用自定义映射器类。你可以在 dto/mapper package 下找到一些示例。

**_DAOs_**

数据访问对象（DAO）位于***repository***  package中。它们都 extends MongoRepository Interface ，帮助服务层持久化并从 MongoDB检索数据。服务层是在 ***servicc***  package下定义的，考虑到当实现的系统（即车票预定系统），有必要创建两个基本服务——UserService 和 BusReservationService，以满足用户执行的不同业务操作。

**_Security_**

与 security 相关的设置都在的***config*** package 中，实际配置在**security package 中的类下完成。应用程序对管理员和 REST API 采用了不同的技术，对于对管理员应用了基于 sessionID 和 cookies 概念的默认 spring 会话机制。对于 REST API，使用了基于 JWT 令牌的身份验证机制。

**_Controllers_**

最重要的部分是控制器层（ controller layer）。它把所有从截获请求的那一刻，一直到准备好并发回响应的东西都绑定在一起。控制器层存在于***controller*** package 中，最佳实践建议我们保持此层的版本以支持应用程序的多个版本，这里也应用了相同的做法。目前代码只在v1下出现，但随着时间的推移，我希望有不同的版本、不同的特性。与管理员相关的控制器位于***ui*** package 中，其相关的表单控制对象位于***command*** package 下。 REST API 的控制器位于 ***api*** package 下，相应的请求类位于**_request_** pacakge 中。

**_Request and Form Commands_**

各位同仁在是否需要使用不同的类来映射传入的请求与使用DTO之间有不同的观点。就我个人而言我是希望尽可能地将这两个类分开来，以保证 UI 和 Controller 之间的松耦合。request 对象和表单命令确实为我们提供了一个可以在他们到达 DTO 层之前做一些额外的数据验证。我们也可以直接用 DTO 来进行数据验证（确实有人喜欢这种方法），因为它减少了一些额外的类，但是我通常更喜欢将验证逻辑与传输对象分开，因此倾向于在它们之前使用请求/命令对象。



静态资源都在 ***resources*** 文件夹下. 所有UI对象及其样式方面都可以在这里找到。

## Response and Exception Handling ##
I have tried to experiment a bit with the RuntimeExceptions and come up with a mini framework for handling the entire application's exceptions using a few classes and the properties file. If you carefully observe the **_exception_** package, it consists of two enums - EntityType and ExceptionType. The EntityType enum contains all the entity names that we are using in the system for persistence and those which can result in a run time exception. The ExceptionType enum consists of the different entity level exceptions such as the EntityNotFound and DuplicateEntity exceptions. 

The BRSException class has two static classes _EntityNotFoundException_ and _DuplicateEntityException_ which are the two most widely thrown exceptions from the service layer. It also contains a set of overloaded methods _throwException_ which take the EntityType, ExceptionType and arguments to come up with a formatted message whose template is present under the **_custom.properties_** file. Using this class I was able to empower the entire services layer to throw entity exceptions in a uniform manner without cluttering the code base with all sorts of NOT_FOUND and DUPLICATE entity exceptions.

For example, while login if you try to use a email address which is not registered, an exception is raised and thrown using the following single line of code -

``` java
throw exception(USER, ENTITY_NOT_FOUND, userDto.getEmail());
```

This results in clubbing the names of these two enums USER(user) and ENTITY_NOT_FOUND(not.found) and coming up with a key _user.not.found_ which is present in the custom.properties files as follows :

``` java
user.not.found=Requested user with email - {0} does not exist.
```
By simply replacing the {0} param with the email address included in the thrown exception you can get a well formatted message to be shown to the user or to be sent back as the response of the REST API call.

Another important part of this mini framework is the **_CustomizedResponseEntityExceptionHandler_** class. This class takes care of these RuntimeExceptions before sending a response to the API requests. Its a controller advice that checks if a service layer invocation resulted in a EntityNotFoundException or a DuplicateEntityException and sends an appropriate response to the caller.

Last, the API response are all being sent in a uniform manner using the **_Response_** class present in the dto/response package. This class allows us to create uniform objects which result in a response as shown below (this one is a response for the "api/v1/reservation/stops" api) :

```json
{
    "status": "OK",
    "payload": [
        {
            "code": "STPA",
            "name": "Stop A",
            "detail": "Near hills"
        },
        {
            "code": "STPB",
            "name": "Stop B",
            "detail": "Near river"
        }
    ]
}
```

And when there is an exception (for example searching for a trip between two stops which are not linked by any bus) the following responses are sent back (result of "api/v1/reservation/tripsbystops" GET request) :

```json
{
    "status": "NOT_FOUND",
    "errors": "No trips between source stop - 'STPD' and destination stop - 'STPC' are available at this time."
}
```

```json
{
    "status": "NOT_FOUND",
    "errors": {
        "timestamp": "2019-03-13T07:47:10.990+0000",
        "message": "Requested stop with code - STPF does not exist.",
        "details": "Requested stop with code - STPF does not exist."
    }
}
```

As you can observe, both type of responses, one with a HTTP-200 and another with HTTP-404 the response payload doesn't change its structure and the calling framework can blindly accept the response knowing that there is a status and a error or payload field in the JSON object.

## UI Architecture ##
The user interface for the admin portal is designed using material design with the help of Bootstrap and responsive web app concept. The UI is server side rendered using Thymeleaf templates (preferred templating engine in Spring). The standard way of working with Thymeleaf is to use includes. This quite often leads to repetitive code, especially, when a website has many pages and each page has several reusable components (e.g. header, navigation, sidebar, and footer). It is repetitive as each content page has to include the same fragments at the same locations. This also has a negative effect when the page layout changes, e.g. when putting the sidebar from the left to the right side.

The decorator pattern used by the Thymeleaf Layout dialect solves these issues. In the context of template engines, the decorator pattern doesn't work with includes on content pages anymore, but it refers to a common template file. Each page basically only provides the main content and by describing which basic template to use the template engine can build the final page. The content is being decorated with the template file.This approach has advantages compared to the standard way of including fragments:

- The page itself only has to provide the content
- As a template file is being used to build the final page global changes can be applied easily
- The code becomes shorter and cleaner
- As each content page references which template file to use, it is easy to use different templates for different areas of the application (e.g. public area and admin area)

The layout for admin portal is arranged as follows :

<p align="center">
<img width="600" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/ui-layout.png">
</p>

The individual areas in this layout serve the following purpose :

- **Header**: this fragment is used for the static imports (CSS and JavaScript), the title and meta tags
- **Navigation**: the navigation bar
- **Content**: the content placeholder that will be replaced by the requested page
- **Sidebar**: a sidebar for additional information
- **Footer**: the footer area that provides the copyright info

These components can be located in the resources/templates directory at the root as well as under the sub-directories fragments and layout. The content area in this layout will host the following pages :

- Dashboard
- Agency
- Bus
- Trip
- Profile

Also, an error page for any unhandled exception is designed with the name "error.html". The login and signup pages are designed separately from the portal accessible to a logged-in user.

## Running the server locally ##
To be able to run this Spring Boot app you will need to first build it. To build and package a Spring Boot app into a single executable Jar file with a Maven, use the below command. You will need to run it from the project folder which contains the pom.xml file.

```
maven package
```
or you can also use

```
mvn install
```

To run the Spring Boot app from a command line in a Terminal window you can you the java -jar command. This is provided your Spring Boot app was packaged as an executable jar file.

```
java -jar target/springboot-starterkit-0.0.1-SNAPSHOT.jar
```

You can also use Maven plugin to run the app. Use the below example to run your Spring Boot app with Maven plugin :

```
mvn spring-boot:run
```

If you do not have a mongo instance running and still just want to create the JAR, then please use the following command:

```
mvn install -DskipTests
```

This will skip the test cases and won't check the availability of a mongodb instance and allow you to create the JAR.

You can follow any/all of the above commands, or simply use the run configuration provided by your favorite IDE and run/debug the app from there for development purposes. Once the server is setup you should be able to access the admin interface at the following URL :

http://localhost:8080

And the REST APIs can be accessed over the following base-path :

http://localhost:8080/api/

Some of the important api endpoints are as follows :

- http://localhost:8080/api/v1/user/signup (HTTP:POST)
- http://localhost:8080/api/auth (HTTP:POST)
- http://localhost:8080/api/v1/reservation/stops (HTTP:GET)
- http://localhost:8080/api/v1/reservation/tripsbystops (HTTP:GET)
- http://localhost:8080/api/v1/reservation/tripschedules (HTTP:GET)
- http://localhost:8080/api/v1/reservation/bookticket (HTTP:POST)

## Running the server in Docker Container ##
##### Docker #####
Command to build the container :

```
docker build -t spring/starterkit .
```

Command to run the container :

```
docker run -p 8080:8080 spring/starterkit
```

Please **note** when you build the container image and if mongodb is running locally on your system, you will need to provide your system's IP address (or cloud hosted database's IP) in the application.properties file to be able to connect to the database from within the container.

##### Docker Compose #####
Another alternative to run the application is to use the docker-compose.yml file and utility. To build the application using docker-compose simply execute the following command :
```
docker-compose build
```

And to run the application, please execute the following command :
```
docker-compose up
```

## API Documentation ##
Its as important to document(as is the development) and make your APIs available in a readable manner for frontend teams or external consumers. The tool for API documentation used in this starter kit is Swagger2, you can open the same inside a browser at the following url -

http://localhost:8080/swagger-ui.html

It will present you with a well structured UI which has two specs :

1. User
2. BRS

You can use the User spec to execute the login api for generating the Bearer token. The token then should be applied in the "Authorize" popup which will by default apply it to all secured apis (get and post both).

<p align="center">
    <b>User Spec</b><br>
    <br>
    <img width="600" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/swagger-screens/swagger-1.png">
</p>

<p align="center">
    <b>User Login</b><br>
    <br>
    <img width="600" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/swagger-screens/swagger-2.png">
</p>

<p align="center">
    <b>Authorization</b><br>
    <br>
    <img width="600" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/swagger-screens/swagger-3.png">
</p>

<p align="center">
    <b>BRS Spec</b><br>
    <br>
    <img width="600" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/swagger-screens/swagger-4.png">
</p>

<p align="center">
    <b>BRS APIs</b><br>
    <br>
    <img width="600" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/swagger-screens/swagger-5.png">
</p>

The configuration of Swagger is being taken care of by class BrsConfiguration. I have defined two specs there with the help of "swaggerBRSApi" and "swaggerUserApi" methods. Since the login part is by default taken care of by Spring Security we don't get to expose its apis implicitly as the rest of the apis defined in the system and for the same reason I have defined a controller in the config package with the name "FakeController". Its purpose is to facilitate the generation of swagger documentation for login and logout apis, it will never come into existence during the application life cycle as the "/api/auth" api is being handled by the security filters defined in the code base. 

## User Interface ##
Here are the various screens of the Admin portal that you should be able to use once the application is setup properly :


<p align="center">
    <b>Login</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/login.png">
</p>

<p align="center">
    <b>Signup</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/signup.png">
</p>

<p align="center">
    <b>Dashboard</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/dashboard.png">
</p>

<p align="center">
    <b>Agency</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/agency.png">
</p>

<p align="center">
    <b>Buses</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/buses.png">
</p>

<p align="center">
    <b>Trips</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/trips.png">
</p>

<p align="center">
    <b>Profile</b><br>
    <br>
    <img width="800" src="https://github.com/khandelwal-arpit/springboot-starterkit/blob/master/docs/images/app-screens/profile.png">
</p>

## Contributors ##
[Arpit Khandelwal](https://www.linkedin.com/in/arpitkhandelwal1984/)

## License ##
This project is licensed under the terms of the MIT license.