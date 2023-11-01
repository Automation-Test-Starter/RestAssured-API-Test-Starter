
# RestAssured 接口自动化测试开始启动项目

关于使用 RestAssured 进行 API 测试的快速启动项目介绍文档。

**中文** | [English](/README_EN.md)

- [RestAssured 接口自动化测试开始启动项目](#restassured-接口自动化测试开始启动项目)
  - [RestAssured 介绍](#restassured-介绍)
  - [项目结构](#项目结构)
    - [Gradle 构建的版本](#gradle-构建的版本)
    - [Maven 构建的版本](#maven-构建的版本)
  - [项目依赖](#项目依赖)
  - [从 0 到 1 搭建 REST Assured 接口测试项目](#从-0-到-1-搭建-rest-assured-接口测试项目)
    - [Gradle 版本](#gradle-版本)
      - [创建一个空的 Gradle 工程](#创建一个空的-gradle-工程)
      - [配置项目 build.gradle](#配置项目-buildgradle)
      - [testng.xml 配置](#testngxml-配置)
      - [gradle build 项目并初始化](#gradle-build-项目并初始化)
      - [初始化目录](#初始化目录)
      - [demo 测试接口](#demo-测试接口)
        - [Get 接口](#get-接口)
        - [Post 接口](#post-接口)
      - [编写脚本](#编写脚本)
      - [调试脚本](#调试脚本)
      - [查看测试报告](#查看测试报告)
        - [命令行报告](#命令行报告)
        - [testng html 报告](#testng-html-报告)
    - [Maven 版本](#maven-版本)
      - [创建一个空的 Maven 工程](#创建一个空的-maven-工程)
      - [配置项目 pom.xml](#配置项目-pomxml)
      - [testng.xml 配置](#testngxml-配置-1)
      - [初始化目录](#初始化目录-1)
      - [demo 测试接口](#demo-测试接口-1)
        - [Get 接口](#get-接口-1)
        - [Post 接口](#post-接口-1)
      - [编写脚本](#编写脚本-1)
      - [调试脚本](#调试脚本-1)
      - [查看测试报告](#查看测试报告-1)
        - [命令行报告](#命令行报告-1)
        - [testng html 报告](#testng-html-报告-1)
  - [进阶用法](#进阶用法)
    - [验证响应数据](#验证响应数据)
      - [响应体断言](#响应体断言)
        - [json 格式断言](#json-格式断言)
        - [xml 格式断言](#xml-格式断言)
      - [Cookie 断言](#cookie-断言)
      - [状态码 Status Code 断言](#状态码-status-code-断言)
      - [Header 断言](#header-断言)
      - [Content-Type 断言](#content-type-断言)
      - [内容全匹配断言](#内容全匹配断言)
      - [响应时间断言](#响应时间断言)
    - [文件上传](#文件上传)
    - [Logging 日志](#logging-日志)
      - [全局日志配置](#全局日志配置)
        - [添加全局日志步骤](#添加全局日志步骤)
        - [全局日志代码示例](#全局日志代码示例)
        - [查看全局日志输出](#查看全局日志输出)
      - [局部日志配置](#局部日志配置)
        - [添加日志步骤](#添加日志步骤)
        - [局部日志代码示例](#局部日志代码示例)
        - [查看局部日志输出](#查看局部日志输出)
      - [LogConfig 配置说明](#logconfig-配置说明)
      - [Request Logging 请求日志记录](#request-logging-请求日志记录)
      - [Response Logging 响应日志记录](#response-logging-响应日志记录)
      - [只在验证失败时记录日志](#只在验证失败时记录日志)
      - [Header 黑名单配置](#header-黑名单配置)
    - [Filters 过滤器](#filters-过滤器)
      - [Ordered Filters 有序过滤器](#ordered-filters-有序过滤器)
      - [Response Builder 响应生成器](#response-builder-响应生成器)
    - [持续集成](#持续集成)
      - [接入 github action](#接入-github-action)
        - [Gradle 版本接入 github action](#gradle-版本接入-github-action)
        - [Maven 版本接入 github action](#maven-版本接入-github-action)
    - [集成 allure 测试报告](#集成-allure-测试报告)
      - [allure 简介](#allure-简介)
      - [集成步骤](#集成步骤)
        - [Maven 版本集成 allure](#maven-版本集成-allure)
        - [Gradle 版本集成 allure](#gradle-版本集成-allure)
  - [参考资料](#参考资料)

## RestAssured 介绍

REST Assured 是一种用于测试 RESTful API 的 Java 测试框架，它使开发人员/测试人员能够轻松地编写和执行 API 测试。它的设计旨在使 API 测试变得简单和直观，同时提供了丰富的功能和灵活性。以下是 REST Assured 的一些重要特点和用法：

1. 发起 HTTP 请求：REST Assured 允许你轻松地构建和发起 HTTP GET、POST、PUT、DELETE 等类型的请求。你可以指定请求的 URL、头部、参数、体等信息。

2. 链式语法：REST Assured 使用链式语法，使测试代码更加可读和易于编写。你可以按照一种自然的方式描述你的测试用例，而不需要编写大量的代码。

3. 断言和校验：REST Assured 提供了丰富的校验方法，可以用于验证 API 响应的状态码、响应体、响应头等。你可以根据你的测试需求添加多个断言。

4. 支持多种数据格式：REST Assured 支持多种数据格式，包括 JSON、XML、HTML、Text 等。你可以使用适当的方法来处理不同格式的响应数据。

5. 集成 BDD（行为驱动开发）：REST Assured 可以与 BDD 框架（如 Cucumber）结合使用，使你可以更好地描述和管理测试用例。

6. 模拟 HTTP 服务器：REST Assured 还包括一个模拟 HTTP 服务器的功能，允许你模拟 API 的行为以进行端到端测试。

7. 可扩展性：REST Assured 可以通过插件和扩展进行定制，以满足特定的测试需求。

总的来说，REST Assured 是一个功能强大且易于使用的 API 测试框架，它可以帮助你轻松地进行 RESTful API 测试，并提供了许多工具来验证 API 的正确性和性能。无论是初学者还是有经验的开发人员/测试人员，REST Assured 都是一个非常有价值的工具，可用于快速的上手 API 自动化 测试。

## 项目结构

### Gradle 构建的版本

```text
- src
  - main
    - java
      - (应用的主要源代码)
  - test
    - java
      - api
        - (REST Assured 测试代码)
          - UsersAPITest.java
          - ProductsAPITest.java
        - util
          - TestConfig.java
    - resources
      - (配置文件、测试数据等)
  - (其他项目文件和资源)
- build.gradle (Gradle 项目配置文件)
```

在这个示例目录结构中：

- src/test/java/api 目录用于存放 REST Assured 的测试类，每个测试类通常涉及到一个或多个相关的 API 端点的测试。例如，UsersAPITest.java 和 ProductsAPITest.java 可以包含用户管理和产品管理的测试。
- src/test/java/util 目录可用于存放测试中共享的工具类，例如用于配置 REST Assured 的 TestConfig.java。
- src/test/resources 目录可以包含测试数据文件、配置文件等资源，这些资源可以在测试中使用。
- build.gradle 是 gradle 项目的配置文件，它用于定义项目的依赖项、构建配置以及其他项目设置。

### Maven 构建的版本

```text
- src
  - main
    - java
      - (应用的主要源代码)
  - test
    - java
      - api
        - (REST Assured 测试代码)
          - UsersAPITest.java
          - ProductsAPITest.java
        - util
          - TestConfig.java
    - resources
      - (配置文件、测试数据等)
  - (其他项目文件和资源)
- pom.xml (Maven 项目配置文件)
```

在这个示例目录结构中：

- src/test/java/api 目录用于存放 REST Assured 的测试类，每个测试类通常涉及到一个或多个相关的 API 端点的测试。例如，UsersAPITest.java 和 ProductsAPITest.java 可以包含用户管理和产品管理的测试。
- src/test/java/util 目录可用于存放测试中共享的工具类，例如用于配置 REST Assured 的 TestConfig.java。
- src/test/resources 目录可以包含测试数据文件、配置文件等资源，这些资源可以在测试中使用。
- pom.xml 是 Maven 项目的配置文件，它用于定义项目的依赖项、构建配置以及其他项目设置。

## 项目依赖

- JDK 1.8+ ，我使用的 JDK 19
- Gradle 6.0+ 或 Maven 3.0+，我使用的 Gradle 8.44 和 Maven 3.9.5
- RestAssured 4.3.3+，我使用的是最新的 5.3.1 版本

## 从 0 到 1 搭建 REST Assured 接口测试项目

REST Assured 支持 Gradle 和 Maven 两种构建工具，你可以根据自己的喜好选择其中一种。下面分别介绍 Gradle 和 Maven 两种构建工具的项目初始化过程。

本项目使用 Gradle 8.44 和 Maven 3.9.5 进行构建，如果你使用的是其他版本，可能会有不同。

### Gradle 版本

可参考 demo 项目：<https://github.com/Automation-Test-Starter/RestAssured-gradle-demo>

#### 创建一个空的 Gradle 工程

```bash
mkdir RestAssured-gradle-demo
cd RestAssured-gradle-demo
gradle init
```

#### 配置项目 build.gradle

demo 项目引入了 testNG 测试框架，仅供参考

- 在项目根目录下创建一个 build.gradle 文件，用于配置项目
- 示例配置如下，可供参考

```groovy
// 插件配置
plugins {
    id 'java' // 使用 java 插件
}

// 仓库资源配置
repositories {
  mavenCentral() // 使用 maven中央版本库源
}

// 项目依赖配置
dependencies {
    testImplementation 'io.rest-assured:rest-assured:5.3.1' // 添加rest-assured依赖
    testImplementation 'org.testng:testng:7.8.0' // 添加TestNG测试框架依赖
    implementation 'org.uncommons:reportng:1.1.4' // 添加testng 测试报告依赖
    implementation 'org.slf4j:slf4j-api:2.0.9' // 添加测试日志依赖
    implementation 'org.slf4j:slf4j-simple:2.0.9' // 添加测试日志依赖
    implementation group: 'com.google.inject', name: 'guice', version: '7.0.0'
}

// 项目测试配置
test {
    reports.html.required = false // 禁用 gradle 原生HTML 报告生成
    reports.junitXml.required = false // 禁用 gradle 原生 JUnit XML 报告生成
    // 告诉 Gradle 使用 TestNG 作为测试框架
    useTestNG() {
        useDefaultListeners = true
        suites 'src/test/resources/testng.xml' // 声明 testng 的 xml 配置文件路径
    }
    testLogging.showStandardStreams = true // 将测试日志输出到控制台
    testLogging.events "passed", "skipped", "failed" // 定义测试日志事件类型
}
```

> 可 copy 本项目中的 build.gradle 文件内容，更多配置可参考[官方文档](https://github.com/rest-assured/rest-assured/wiki/GettingStarted#rest-assured)

#### testng.xml 配置

- 在 src/test目录下创建一个 resources 目录，用于存放测试配置文件

- 在 resources 目录下创建一个 testng.xml 文件，用于配置 TestNG 测试框架

- 示例配置如下，可供参考

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="restAssured-gradleTestSuite">
<test thread-count="1" name="Demo">
    <classes>
        <class name="com.example.TestDemo"/> <!-- 测试脚本 class-->
    </classes>
</test> <!-- Test -->
</suite> <!-- Suite -->
```

#### gradle build 项目并初始化

- 用编辑器打开本项目 Terminal 窗口，执行以下命令确认项目 build 成功

```bash
gradle build
```

- 初始化完成：完成向导后，Gradle 将在项目目录中生成一个基本的 Gradle 项目结构
  
#### 初始化目录

目录结构可参考 >> [项目结构](#项目结构)

在项目的测试源目录下创建一个新的测试类。默认情况下，Gradle 通常将测试源代码放在 src/test/java 目录中。你可以在该目录下创建测试类的包，并在包中创建新的测试类

创建一个 TestDemo 的测试类，可以按以下结构创建文件
  
```text
src
└── test
    └── java
        └── com
            └── example
                └── TestDemo.java
```

#### demo 测试接口

##### Get 接口

- HOST: https://jsonplaceholder.typicode.com
- 接口地址：/posts/1
- 请求方式：GET
- 请求参数：无
- 请求头："Content-Type": "application/json; charset=utf-8"
- 请求体：无
- 返回状态码：200
- 返回头："Content-Type": "application/json; charset=utf-8"
- 返回 body：

```json
{
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

##### Post 接口

- HOST: https://jsonplaceholder.typicode.com
- 接口地址：/posts
- 请求方式：POST
- 请求参数：无
- 请求头："Content-Type": "application/json; charset=utf-8"
- 请求体：raw json 格式 body 内容如下：

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
```

- 返回状态码：201
- 返回头："Content-Type": "application/json; charset=utf-8"
- 返回 body：

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1,
    "id": 101
}
```

#### 编写脚本

- 打开 TestDemo.java 文件，开始编写测试脚本

- 示例脚本如下，可供参考

```java
package com.example;

import org.testng.annotations.Test;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

public class TestDemo {

 @Test(description = "Verify that the Get Post API returns correctly")
 public void verifyGetAPI() {

  // Given
  given()
    .baseUri("https://jsonplaceholder.typicode.com")
             .header("Content-Type", "application/json")

  // When
  .when()
    .get("/posts/1")

  // Then
  .then()
    .statusCode(200)
    // To verify correct value
    .body("userId", equalTo(1))
    .body("id", equalTo(1))
    .body("title", equalTo("sunt aut facere repellat provident occaecati excepturi optio reprehenderit"))
    .body("body", equalTo("quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"));
 }
 @Test(description = "Verify that the publish post API returns correctly")
 public void verifyPostAPI() {

  // Given
  given()
    .baseUri("https://jsonplaceholder.typicode.com")
    .header("Content-Type", "application/json")

    // When
    .when()
    .body("{\"title\": \"foo\", \"body\": \"bar\", \"userId\": 1\n}")
    .post("/posts")

    // Then
    .then()
    .statusCode(201)
    // To verify correct value
    .body("userId", equalTo(1))
    .body("id", equalTo(101))
    .body("title", equalTo("foo"))
    .body("body", equalTo("bar"));
 }
}
```

#### 调试脚本

- 打开本项目的 Terminal 窗口，执行以下命令运行测试脚本

```bash
gradle test
```

#### 查看测试报告

##### 命令行报告

![gradle-test-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/gradle-report1.png)

##### testng html 报告

- 打开项目 build/reports/tests/test 目录
- 点击 index.html 文件，查看测试报告

![gradle-test-report2](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/gradle-report2.png)

### Maven 版本

可参考 demo 项目：<https://github.com/Automation-Test-Starter/RestAssured-maven-demo>

#### 创建一个空的 Maven 工程

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=RestAssured-maven-demo -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

初始化完成：完成向导后，Maven 将在新建项目目录并生成一个基本的 Maven 项目结构

#### 配置项目 pom.xml

在 项目中 pom.xml 文件中添加以下内容

> 可 copy 本项目中的 pom.xml 文件内容，更多配置可参考[官方文档](https://github.com/rest-assured/rest-assured/wiki/GettingStarted#rest-assured)

```xml
<!-- 依赖配置 -->
  <dependencies>
    <!-- https://mvnrepository.com/artifact/io.rest-assured/rest-assured -->
    <dependency>
      <groupId>io.rest-assured</groupId>
      <artifactId>rest-assured</artifactId>
      <version>5.3.1</version>
      <scope>test</scope>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.testng/testng -->
    <dependency>
      <groupId>org.testng</groupId>
      <artifactId>testng</artifactId>
      <version>7.8.0</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  <!-- 插件配置 -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.2.1</version>
        <configuration>
          <suiteXmlFiles>
            <suiteXmlFile>src/test/resources/testng.xml</suiteXmlFile>
          </suiteXmlFiles>
        </configuration>
      </plugin>
```

#### testng.xml 配置

- 在 src/test目录下创建一个 resources 目录，用于存放测试配置文件

- 在 resources 目录下创建一个 testng.xml 文件，用于配置 TestNG 测试框架

- 示例配置如下，可供参考

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="restAssured-gradleTestSuite">
<test thread-count="1" name="Demo">
    <classes>
        <class name="com.example.TestDemo"/> <!-- 测试脚本 class-->
    </classes>
</test> <!-- Test -->
</suite> <!-- Suite -->
```

#### 初始化目录

目录结构可参考 >> [项目结构](#项目结构)

在项目的测试源目录下创建一个新的测试类。默认情况下，Gradle 通常将测试源代码放在 src/test/java 目录中。你可以在该目录下创建测试类的包，并在包中创建新的测试类

创建一个 TestDemo 的测试类，可以按以下结构创建文件
  
```text
src
└── test
    └── java
        └── com
            └── example
                └── TestDemo.java
```

#### demo 测试接口

##### Get 接口

- HOST: https://jsonplaceholder.typicode.com
- 接口地址：/posts/1
- 请求方式：GET
- 请求参数：无
- 请求头："Content-Type": "application/json; charset=utf-8"
- 请求体：无
- 返回状态码：200
- 返回头："Content-Type": "application/json; charset=utf-8"
- 返回 body：

```json
{
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

##### Post 接口

- HOST: https://jsonplaceholder.typicode.com
- 接口地址：/posts
- 请求方式：POST
- 请求参数：无
- 请求头："Content-Type": "application/json; charset=utf-8"
- 请求体：raw json 格式 body 内容如下：

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
```

- 返回状态码：201
- 返回头："Content-Type": "application/json; charset=utf-8"
- 返回 body：

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1,
    "id": 101
}
```

#### 编写脚本

- 打开 TestDemo.java 文件，开始编写测试脚本

- 示例脚本如下，可供参考

```java
package com.example;

import org.testng.annotations.Test;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

public class TestDemo {

 @Test(description = "Verify that the Get Post API returns correctly")
 public void verifyGetAPI() {

  // Given
  given()
    .baseUri("https://jsonplaceholder.typicode.com")
             .header("Content-Type", "application/json")

  // When
  .when()
    .get("/posts/1")

  // Then
  .then()
    .statusCode(200)
    // To verify correct value
    .body("userId", equalTo(1))
    .body("id", equalTo(1))
    .body("title", equalTo("sunt aut facere repellat provident occaecati excepturi optio reprehenderit"))
    .body("body", equalTo("quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"));
 }
 @Test(description = "Verify that the publish post API returns correctly")
 public void verifyPostAPI() {

  // Given
  given()
    .baseUri("https://jsonplaceholder.typicode.com")
    .header("Content-Type", "application/json")

    // When
    .when()
    .body("{\"title\": \"foo\", \"body\": \"bar\", \"userId\": 1\n}")
    .post("/posts")

    // Then
    .then()
    .statusCode(201)
    // To verify correct value
    .body("userId", equalTo(1))
    .body("id", equalTo(101))
    .body("title", equalTo("foo"))
    .body("body", equalTo("bar"));
 }
}
```

#### 调试脚本

- 打开本项目的 Terminal 窗口，执行以下命令运行测试脚本

```bash
mvn test
```

#### 查看测试报告

##### 命令行报告

![maven-test-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/maven-report1.png)

##### testng html 报告

- 打开项目 target/surefire-reports 目录
- 点击 index.html 文件，查看测试报告

![maven-test-report2](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/maven-report2.png)

## 进阶用法

### 验证响应数据

您还可以验证状态码，状态行，Cookie，headers，内容类型和正文。

#### 响应体断言

##### json 格式断言
  
假设某个 get 请求 (http://localhost:8080/lotto) 返回 JSON 如下：

```json
{
"lotto":{
 "lottoId":5,
 "winning-numbers":[2,45,34,23,7,5,3],
 "winners":[{
   "winnerId":23,
   "numbers":[2,45,34,23,3,5]
 },{
   "winnerId":54,
   "numbers":[52,3,12,11,18,22]
 }]
}
}
```

REST assured 可以帮您轻松地进行 get 请求并对响应信息进行处理。

- 断言 lottoId 的值是否等于 5，示例：

```java
get("/lotto").then().body("lotto.lottoId", equalTo(5));
```

- 断言 winnerId 的取值包括 23 和 54，示例：

```java
get("/lotto").then().body("lotto.winners.winnerId", hasItems(23, 54));
```

> 提醒一下：`equalTo` 和 `hasItems`是 Hamcrest matchers 提供的方法，所以需要静态导入入 `org.hamcrest.Matchers`。

##### xml 格式断言

XML 可以一种通过简单的方式解析。假设一个 POST 请求`http://localhost:8080/greetXML`返回：

```xml
<greeting>
   <firstName>{params("firstName")}</firstName>
   <lastName>{params("lastName")}</lastName>
</greeting>
```

- 断言 firstName 是否返回正确，示例：

```java
given().
         parameters("firstName", "John", "lastName", "Doe").
when().
         post("/greetXML").
then().
         body("greeting.firstName", equalTo("John")).
```

- 同时断言 firstname 和 lastname 是否返回正确，示例：

```java
given().
         parameters("firstName", "John", "lastName", "Doe").
when().
         post("/greetXML").
then().
         body("greeting.firstName", equalTo("John")).
         body("greeting.lastName", equalTo("Doe"));
```

```java
with().parameters("firstName", "John", "lastName", "Doe").when().post("/greetXML").then().body("greeting.firstName", equalTo("John"), "greeting.lastName", equalTo("Doe"));
```

#### Cookie 断言

- 断言 cookie 的值是否等于 cookieValue，示例：

```java
get("/x").then().assertThat().cookie("cookieName", "cookieValue")
```

- 同时断言 多个 cookie 的值是否等于 cookieValue，示例：

```java
get("/x").then().assertThat().cookies("cookieName1", "cookieValue1", "cookieName2", "cookieValue2")
```

- 断言 cookie 的值是否包含 cookieValue，示例：

```java
get("/x").then().assertThat().cookies("cookieName1", "cookieValue1", "cookieName2", containsString("Value2"))
```

#### 状态码 Status Code 断言

- 断言 状态码是否等于 200，示例：

```java
get("/x").then().assertThat().statusCode(200)
```

- 断言 状态行是否为 something，示例：

```java
get("/x").then().assertThat().statusLine("something")
```

- 断言 状态行是否包含 some，示例：

```java
get("/x").then().assertThat().statusLine(containsString("some"))
```

#### Header 断言

- 断言 Header 的值是否等于 HeaderValue，示例：

```java
get("/x").then().assertThat().header("headerName", "headerValue")
```

- 同时断言 多个 Header 的值是否等于 HeaderValue，示例：

```java
get("/x").then().assertThat().headers("headerName1", "headerValue1", "headerName2", "headerValue2")
```

- 断言 Header 的值是否包含 HeaderValue，示例：

```java
get("/x").then().assertThat().headers("headerName1", "headerValue1", "headerName2", containsString("Value2"))
```

- 断言 Header 的“Content-Length”小于 1000，示例：

> 可以先使用映射函数首先将头值转换为 int，然后在使用 Hamcrest 验证前使用“整数”匹配器进行断言：

```java
get("/something").then().assertThat().header("Content-Length", Integer::parseInt, lessThan(1000));
```

#### Content-Type 断言

- 断言 Content-Type 的值是否等于 application/json，示例：

```java
get("/x").then().assertThat().contentType(ContentType.JSON)
```

#### 内容全匹配断言

- 断言 响应体是否完全等于 something，示例：

```java
get("/x").then().assertThat().body(equalTo("something"))
```

#### 响应时间断言

> REST Assured  2.8.0 开始支持测量响应时间，例如：

```java
long timeInMs = get("/lotto").time()
```

或使用特定时间单位：

```java
long timeInSeconds = get("/lotto").timeIn(SECONDS);

```

其中 SECONDS 只是一个标准的 TimeUnit。您还可以使用 DSL 验证：

```java
when().
      get("/lotto").
then().
      time(lessThan(2000L)); // Milliseconds
```

或

```java
when().
      get("/lotto").
then().
      time(lessThan(2L), SECONDS);
```

需要注意的是，您只能参考性地将这些测量数据与服务器请求处理时间相关联（因为响应时间将包括 HTTP 往返和 REST Assured 处理时间等，不能做到十分准确）。

### 文件上传

通常我们在向服务器传输大容量的数据时，比如文件时会使用 multipart 表单数据技术。
rest-assured 提供了一种`multiPart`方法来辨别这究竟是文件、二进制序列、输入流还是上传的文本。

- 表单中上只传一个文件，示例：

```java
given().
        multiPart(new File("/path/to/file")).
when().
        post("/upload");
```

- 存在 control 名的情况下上传文件，示例：

```java
given().
        multiPart("controlName", new File("/path/to/file")).
when().
        post("/upload");
```

- 同一个请求中存在多个"multi-parts"事务，示例：

```java
byte[] someData = ..
given().
        multiPart("controlName1", new File("/path/to/file")).
        multiPart("controlName2", "my_file_name.txt", someData).
        multiPart("controlName3", someJavaObject, "application/json").
when().
        post("/upload");
```

- MultiPartSpecBuilder 用法，示例：

> 更多使用方法可以使用[MultiPartSpecBuilder](http://static.javadoc.io/io.rest-assured/rest-assured/3.0.1/io/restassured/builder/MultiPartSpecBuilder.html)：

```java
Greeting greeting = new Greeting();
greeting.setFirstName("John");
greeting.setLastName("Doe");

given().
        multiPart(new MultiPartSpecBuilder(greeting, ObjectMapperType.JACKSON_2)
                .fileName("greeting.json")
                .controlName("text")
                .mimeType("application/vnd.custom+json").build()).
when().
        post("/multipart/json").
then().
        statusCode(200);
```

- MultiPartConfig 用法，示例：

>[MultiPartConfig](http://static.javadoc.io/io.rest-assured/rest-assured/3.0.1/io/restassured/config/MultiPartConfig.html)可用来指定默认的 control 名和文件名

```java
given().config(config().multiPartConfig(multiPartConfig().defaultControlName("something-else")))  
```

> 默认把 control 名配置为"something-else"而不是"file"。
> 更多用法查看 [博客介绍](http://blog.jayway.com/2011/09/15/multipart-form-data-file-uploading-made-simple-with-rest-assured/)

### Logging 日志

当我们在编写接口测试脚本的时候，我们可能需要在测试过程中打印一些日志，以便于我们在测试过程中查看接口的请求和响应信息，以及一些其他的信息。RestAssured 提供了一些方法来打印日志，我们可以根据需要选择合适的方法来打印日志。

- RestAssured 提供了一个全局的日志配置方法，可以在测试开始前配置日志，然后在测试过程中打印日志。这种方法适用于所有的测试用例，但是它只能打印请求和响应的信息，不能打印其他的信息。

- RestAssured 还提供了一个局部的日志配置方法，可以在测试过程中打印日志。这种方法可以打印请求和响应的信息，也可以打印其他的信息。

#### 全局日志配置

##### 添加全局日志步骤

- 引入日志相关的依赖类
  
```java
import io.restassured.config.LogConfig;
import io.restassured.filter.log.LogDetail;
import io.restassured.filter.log.RequestLoggingFilter;
import io.restassured.filter.log.ResponseLoggingFilter;
```

- 在 setup() 方法中添加日志配置

> 使用 LogConfig 配置，启用了请求和响应的日志记录，以及启用了漂亮的输出格式。启用了请求和响应的日志记录过滤器，这将记录请求和响应的详细信息。

```java
// 启用全局请求和响应日志记录
        RestAssured.config = RestAssured.config()
                .logConfig(LogConfig.logConfig()
                        .enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
                        .enablePrettyPrinting(true));
```

- 在 setup() 方法中启用了全局日志记录过滤器

```java
// 启用全局请求和响应日志记录过滤器
    RestAssured.filters(new RequestLoggingFilter(), new ResponseLoggingFilter());
```

##### 全局日志代码示例

```java
package com.example;

import io.restassured.RestAssured;
// 引入日志相关的类
import io.restassured.config.LogConfig;
import io.restassured.filter.log.LogDetail;
import io.restassured.filter.log.RequestLoggingFilter;
import io.restassured.filter.log.ResponseLoggingFilter;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

public class TestDemo {

    @BeforeClass
    public void setup() {
        // 启用全局请求和响应日志记录
        RestAssured.config = RestAssured.config()
                .logConfig(LogConfig.logConfig()
                        .enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
                        .enablePrettyPrinting(true));
        // 启用全局请求和响应日志记录过滤器
        RestAssured.filters(new RequestLoggingFilter(), new ResponseLoggingFilter());
    }

    @Test(description = "Verify that the Get Post API returns correctly")
    public void verifyGetAPI() {
      // 测试用例已省略，可参考 demo
    }

    @Test(description = "Verify that the publish post API returns correctly")
    public void verifyPostAPI() {
      // 测试用例已省略，可参考 demo
    }
}
```

##### 查看全局日志输出

- 打开本项目的 Terminal 窗口，执行以下命令运行测试脚本
- 查看日志输出

![log-sceenshot1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/9Mh9Z8.png)

#### 局部日志配置

在 RestAssured 中，你可以进行局部日志配置，以便在特定的测试方法或请求中启用或禁用日志记录，而不影响全局配置。

##### 添加日志步骤

- 引入日志相关的依赖类
  
```java
import io.restassured.config.LogConfig;
import io.restassured.filter.log.LogDetail;
import io.restassured.filter.log.RequestLoggingFilter;
import io.restassured.filter.log.ResponseLoggingFilter;
```

- 在 setup() 方法中添加日志配置

> 使用 LogConfig 配置，启用了请求和响应的日志记录，以及启用了漂亮的输出格式。启用了请求和响应的日志记录过滤器，这将记录请求和响应的详细信息。

```java
// 启用局部请求和响应日志记录
        // 在 @BeforeClass 中定义 LogConfig 配置
        logConfig = LogConfig.logConfig()
                .enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
                .enablePrettyPrinting(true);
```

- 在 想要打印日志的测试方法中启用了局部日志记录过滤器

```java
    @Test(description = "Verify that the Get Post API returns correctly")
    public void verifyGetAPI() {

        // Given
        given()
                .config(RestAssured.config().logConfig(logConfig))
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .get("/posts/1")

                // Then
                .then()
                .statusCode(200)
    }
```

##### 局部日志代码示例

```java
package com.example;

import io.restassured.RestAssured;
import io.restassured.config.LogConfig;
import io.restassured.filter.log.LogDetail;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

public class TestDemo {
    private LogConfig logConfig;

    @BeforeClass
    public void setUp() {
        // 在 @BeforeClass 中定义 LogConfig 配置
        logConfig = LogConfig.logConfig()
                .enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
                .enablePrettyPrinting(true);
    }
    @Test(description = "Verify that the Get Post API returns correctly")
    public void verifyGetAPI() {

        // Given
        given()
                .config(RestAssured.config().logConfig(logConfig))
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .get("/posts/1")

                // Then
                .then()
                .statusCode(200)
    }
}
```

##### 查看局部日志输出

- 打开本项目的 Terminal 窗口，执行以下命令运行测试脚本
- 查看日志输出
 @Todo

#### LogConfig 配置说明

在 RestAssured 中，你可以使用 `LogConfig` 类来配置请求和响应的日志记录。`LogConfig` 允许你定义日志详细程度、输出格式、输出位置等。以下是一些常见的 `LogConfig` 配置示例：

1. **启用请求和响应的日志记录：**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL));
   ```

   这将启用请求和响应的日志记录，只有当验证失败时才记录。

2. **配置输出级别：**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.HEADERS));
   ```

   这将只记录请求和响应的头部信息。

3. **配置输出位置：**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
           .enablePrettyPrinting(true)
           .defaultStream(FileOutputStream("log.txt")));
   ```

   这将日志记录输出到名为 "log.txt" 的文件。

4. **配置漂亮的输出格式：**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
           .enablePrettyPrinting(true));
   ```

   这将启用漂亮的输出格式，使日志更易于阅读。

你可以根据你的具体需求组合这些配置选项，并将其设置为 `RestAssured.config` 以配置全局的请求和响应日志记录。这将有助于在 RestAssured 中记录和审查请求和响应，以便调试和分析问题。

#### Request Logging 请求日志记录

从版本 1.5 开始，REST Assured 支持在使用 RequestLoggingFilter 将请求规范发送到服务器之前记录请求规范。请注意，HTTP Builder 和 HTTP Client 可能会添加日志中打印的内容之外的其他标头。筛选器将仅记录请求规范中指定的详细信息。也就是说，您不能将 RequestLoggingFilter 记录的详细信息视为实际发送到服务器的详细信息。此外，后续筛选器可能会在日志记录发生后更改请求。如果您需要记录网络上实际发送的内容，请参阅 HTTP 客户端日志记录文档或使用外部工具，例如 Wireshark。

示例：

```java
given().log().all()   // 记录所有请求规范细节，包括参数、标头和正文
given().log().params()   // 只记录请求的参数
given().log().body()   // 只记录请求正文
given().log().headers()   // 只记录请求头
given().log().cookies()   // 只记录请求 cookies
given().log().method()   // 只记录请求方法
given().log().path()   // 只记录请求路径
```

#### Response Logging 响应日志记录

- 只想要打印响应正文，而不考虑状态代码，可以执行以下操作，
示例：

```java
get("/x").then().log().body()
```

- 不管是否发生错误，都将打印响应正文。如果只对在发生错误时打印响应正文感兴趣，示例：

```java
get("/x").then().log().ifError()
```

- 在响应中记录所有详细信息，包括状态行、标头和 Cookie，示例：

```java
get("/x").then().log().all()   
```

- 在响应中记录只记录状态行、标题或 Cookie，示例：

```java
get("/x").then().log().statusLine()   // 只记录状态行
get("/x").then().log().headers()   // 只记录响应头
get("/x").then().log().cookies()   // 只记录响应 cookies
```

- 配置为仅当状态代码与某个值匹配时才记录响应，示例：

```java
get("/x").then().log().ifStatusCodeIsEqualTo(302)   // 仅在状态代码等于 302 时记录日志
get("/x").then().log().ifStatusCodeMatches(matcher)   // 仅在状态代码与提供的配置匹配时才记录日志
```

#### 只在验证失败时记录日志

- 从 REST Assured 2.3.1 开始，只有在验证失败时才能记录请求或响应。要记录请求日志，示例：

```java
given().log().ifValidationFails()
```

- 要记录响应日志，示例：

```java
then().log().ifValidationFails()
```

- 可以使用 LogConfig 同时为请求和响应启用此功能，示例：

```java
given().config(RestAssured.config().logConfig(logConfig().enableLoggingOfRequestAndResponseIfValidationFails(HEADERS)))
```

> 如果验证失败，日志仅记录请求头。

- 另外一个快捷方式，用于在验证失败时为所有请求启用请求和响应的日志记录，示例：
  
```java
RestAssured.enableLoggingOfRequestAndResponseIfValidationFails();
```

- 从版本 4.5.0 开始，您还可以使用 指定 onFailMessage 测试失败时将显示的消息，示例：
  
```java
when().
      get().
then().
      onFailMessage("Some specific message").
      statusCode(200);
```

#### Header 黑名单配置

从 REST Assured 4.2.0 开始，可以将标头列入黑名单，以便它们不会显示在请求或响应日志中。相反，标头值将替换为 [ BLACKLISTED ] .您可以使用 LogConfig 启用此基于每个标头的功能，示例：
  
```java
given().config(config().logConfig(logConfig().blacklistHeader("Accept")))  
```

### Filters 过滤器

在 RestAssured 中，你可以使用过滤器来修改请求和响应。过滤器允许你在请求和响应的不同阶段修改请求和响应。例如，你可以在请求之前修改请求，或者在响应之后修改响应。你可以使用过滤器来添加请求头、请求参数、请求体、响应头、响应体等。

过滤器可用于实现自定义身份验证方案、会话管理、日志记录等。若要创建筛选器，需要实现 io.restassured.filter.Filter 接口。要使用过滤器，您可以执行以下操作：

```java
given().filter(new MyFilter())  
```

REST Assured 提供了几个可供使用的过滤器：

- `io.restassured.filter.log.RequestLoggingFilter` ：将打印请求规范详细信息的筛选器。
- `io.restassured.filter.log.ResponseLoggingFilter` ：如果响应与给定状态代码匹配，则将打印响应详细信息的筛选器。
- `io.restassured.filter.log.ErrorLoggingFilter` ：在发生错误时打印响应正文的筛选器（状态代码介于 400 和 500 之间）。

#### Ordered Filters 有序过滤器

从 REST Assured 3.0.2 开始，如果需要控制筛选器排序，可以实现 io.restassured.filter.OrderedFilter 接口。在这里，您将实现返回一个整数的方法，getOrder 该整数表示筛选器的优先级。值越低，优先级越高。您可以定义的最高优先级是 Integer.MIN_VALUE，最低优先级是 Integer.MAX_VALUE。未实现 io.restassured.filter.OrderedFilter 的过滤器的默认优先级为 1000。

[示例](https://github.com/rest-assured/rest-assured/blob/master/examples/rest-assured-itest-java/src/test/java/io/restassured/itest/java/OrderedFilterITest.java)

#### Response Builder 响应生成器

如果需要更改筛选器中的响应内容，可以使用 ResponseBuilder 基于原始响应创建新的响应。例如，如果要将原始响应的正文更改为其他内容，可以执行以下操作：

```java
Response newResponse = new ResponseBuilder().clone(originalResponse).setBody("Something").build();
```

### 持续集成

#### 接入 github action

以 github action 为例，其他 CI 工具类似

##### Gradle 版本接入 github action

可参考 demo：<https://github.com/Automation-Test-Starter/RestAssured-gradle-demo>

创建.github/workflows 目录：在你的 GitHub 仓库中，创建一个名为 .github/workflows 的目录。这将是存放 GitHub Actions 工作流程文件的地方。

创建工作流程文件：在.github/workflows 目录中创建一个 YAML 格式的工作流程文件，例如 gradle.yml。

编辑 gradle.yml 文件：将以下内容复制到文件中
  
```yaml
name: Gradle and REST Assured Tests

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Java
        uses: actions/setup-java@v3
        with:
          java-version: '11'
          distribution: 'adopt'

      - name: Build and Run REST Assured Tests with Gradle
        uses: gradle/gradle-build-action@bd5760595778326ba7f1441bcf7e88b49de61a25 # v2.6.0
        with:
          arguments: build

      - name: Archive REST-Assured results
        uses: actions/upload-artifact@v2
        with:
          name: REST-Assured-results
          path: build/reports/tests/test

      - name: Upload REST-Assured results to GitHub
        uses: actions/upload-artifact@v2
        with:
          name: REST-Assured-results
          path: build/reports/tests/test
```

- 提交代码：将 gradle.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 Gradle and REST Assured Tests 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果。

![gradle-test-report3](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/gradle-report3.png)

##### Maven 版本接入 github action

可参考 demo：<https://github.com/Automation-Test-Starter/RestAssured-maven-demo>

创建.github/workflows 目录：在你的 GitHub 仓库中，创建一个名为 .github/workflows 的目录。这将是存放 GitHub Actions 工作流程文件的地方。

创建工作流程文件：在.github/workflows 目录中创建一个 YAML 格式的工作流程文件，例如 maven.yml。

编辑 maven.yml 文件：将以下内容复制到文件中
  
```yaml
name: Maven and REST Assured Tests

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  Run-Rest-Assured-Tests:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up JDK 17
      uses: actions/setup-java@v3
      with:
        java-version: '17'
        distribution: 'temurin'
        cache: maven
        
    - name: Build and Run REST Assured Tests with Maven
      run: mvn test
      
    - name: Archive REST-Assured results
      uses: actions/upload-artifact@v3
      with:
        name: REST-Assured-results
        path: target/surefire-reports

    - name: Upload REST-Assured results to GitHub
      uses: actions/upload-artifact@v3
      with:
        name: REST-Assured-results
        path: target/surefire-reports
```

- 提交代码：将 maven.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 Maven and REST Assured Tests 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果。

![maven-test-report3](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/maven-report3.png)

### 集成 allure 测试报告

#### allure 简介

Allure是一个用于生成漂亮、交互式测试报告的开源测试框架。它可以与多种测试框架（如JUnit、TestNG、Cucumber等）和多种编程语言（如Java、Python、C#等）一起使用。

Allure 测试报告具有以下特点：

- 美观和交互式：Allure 测试报告以美观和交互式的方式呈现测试结果，包括图形、图表和动画。这使得测试报告更容易阅读和理解。
- 多语言支持：Allure 支持多种编程语言，因此您可以在不同的语言中编写测试，并生成统一的测试报告。
测试用例级别的详细信息：Allure 允许您为每个测试用例添加详细信息，包括描述、类别、标签、附件、历史数据等。这些信息有助于更全面地了解测试结果。
- 历史趋势分析：Allure 支持测试历史趋势分析，您可以查看测试用例的历史表现，识别问题和改进测试质量。
- 类别和标签：您可以为测试用例添加类别和标签，以更好地组织和分类测试用例。这使得报告更具可读性。
- 附件和截图：Allure 允许您附加文件、截图和其他附件，以便更好地记录测试过程中的信息。
- 集成性：Allure 可以与各种测试框架和构建工具（如 Maven、Gradle）无缝集成，使得生成报告变得简单。
- 开源社区支持：Allure 是一个开源项目，拥有一个活跃的社区，提供了广泛的文档和支持。这使得它成为许多自动化测试团队的首选工具。

Allure 测试报告的主要目标是提供一个清晰、易于阅读的方式来展示测试结果，以帮助开发团队更好地理解测试的状态和质量，快速识别问题，并采取必要的行动。无论您是开发人员、测试人员还是项目经理，Allure 测试报告都能为您提供有用的信息，以改进软件质量和可靠性。

官方网站：<https://docs.qameta.io/allure/>

#### 集成步骤

##### Maven 版本集成 allure

- 在 POM.xml 中添加 allure 依赖

>可 copy 本项目中的 pom.xml 文件内容

```xml
    <!-- https://mvnrepository.com/artifact/io.qameta.allure/allure-testng -->
    <dependency>
      <groupId>io.qameta.allure</groupId>
      <artifactId>allure-testng</artifactId>
      <version>2.24.0</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/io.qameta.allure/allure-rest-assured -->
    <dependency>
      <groupId>io.qameta.allure</groupId>
      <artifactId>allure-rest-assured</artifactId>
      <version>2.24.0</version>
    </dependency>
```

- 在 POM.xml 中添加 allure 插件

```xml
      <plugin>
        <groupId>io.qameta.allure</groupId>
        <artifactId>allure-maven</artifactId>
        <version>2.12.0</version>
        <configuration>
          <resultsDirectory>../allure-results</resultsDirectory>
        </configuration>
      </plugin>
```

- 在 src/test/java 下创建用于测试 REST API 的测试代码

> 以下为 demo 示例，详细部分可参考 项目：<https://github.com/Automation-Test-Starter/RestAssured-maven-demo>

```java
package com.example;

import io.qameta.allure.*;
import io.qameta.allure.restassured.AllureRestAssured;
import org.testng.annotations.Test;
import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

@Epic("REST API Regression Testing using TestNG")
@Feature("Verify that the Get and POST API returns correctly")
public class TestDemo {

    @Test(description = "To get the details of post with id 1", priority = 1)
    @Story("GET Request with Valid post id")
    @Severity(SeverityLevel.NORMAL)
    @Description("Test Description : Verify that the GET API returns correctly")
    public void verifyGetAPI() {

        // Given
        given()
                .filter(new AllureRestAssured()) //设置 AllureRestAssured 过滤器，用来在测试报告中展示请求和响应信息
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .get("/posts/1")

                // Then
                .then()
                .statusCode(200)
                // To verify correct value
                .body("userId", equalTo(1))
                .body("id", equalTo(1))
                .body("title", equalTo("sunt aut facere repellat provident occaecati excepturi optio reprehenderit"))
                .body("body", equalTo("quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"));
    }

    @Test(description = "To create a new post", priority = 2)
    @Story("POST Request")
    @Severity(SeverityLevel.NORMAL)
    @Description("Test Description : Verify that the post API returns correctly")
    public void verifyPostAPI() {        // Given
        given()
                .filter(new AllureRestAssured()) //设置 AllureRestAssured 过滤器，用来在测试报告中展示请求和响应信息
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .body("{\"title\": \"foo\", \"body\": \"bar\", \"userId\": 1\n}")
                .post("/posts")

                // Then
                .then()
                .statusCode(201)
                // To verify correct value
                .body("userId", equalTo(1))
                .body("id", equalTo(101))
                .body("title", equalTo("foo"))
                .body("body", equalTo("bar"));
    }

}
```

- 运行测试并生成 Allure 报告

```bash
mvn clean test
```

> 生成的 Allure 报告在项目根目录的 allure-results 文件下

- 预览 Allure 报告

```bash
mvn allure:serve
```

> 运行命令会自动打开浏览器，预览 Allure 报告

![allure-report](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/JsHrOQ.png)

![allure-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/ZXgnOD.png)

##### Gradle 版本集成 allure

- 在 build.gradle 中添加 allure 插件

>可 copy 本项目中的 build.gradle 文件内容

```groovy
id("io.qameta.allure") version "2.11.2"
```

- 在 build.gradle 中添加 allure 依赖

>可 copy 本项目中的 build.gradle 文件内容

```groovy
    implementation 'io.qameta.allure:allure-testng:2.24.0' // Add allure report dependency
    implementation 'io.qameta.allure:allure-rest-assured:2.24.0' // Add allure report dependency
```

- 在 src/test/java 下创建用于测试 REST API 的测试代码

> 以下为 demo 示例，详细部分可参考 项目：<https://github.com/Automation-Test-Starter/RestAssured-gradle-demo>

```java
package com.example;

import io.qameta.allure.*;
import io.qameta.allure.restassured.AllureRestAssured;
import org.testng.annotations.Test;
import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

@Epic("REST API Regression Testing using TestNG")
@Feature("Verify that the Get and POST API returns correctly")
public class TestDemo {

    @Test(description = "To get the details of post with id 1", priority = 1)
    @Story("GET Request with Valid post id")
    @Severity(SeverityLevel.NORMAL)
    @Description("Test Description : Verify that the GET API returns correctly")
    public void verifyGetAPI() {

        // Given
        given()
                .filter(new AllureRestAssured()) //设置 AllureRestAssured 过滤器，用来在测试报告中展示请求和响应信息
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .get("/posts/1")

                // Then
                .then()
                .statusCode(200)
                // To verify correct value
                .body("userId", equalTo(1))
                .body("id", equalTo(1))
                .body("title", equalTo("sunt aut facere repellat provident occaecati excepturi optio reprehenderit"))
                .body("body", equalTo("quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"));
    }

    @Test(description = "To create a new post", priority = 2)
    @Story("POST Request")
    @Severity(SeverityLevel.NORMAL)
    @Description("Test Description : Verify that the post API returns correctly")
    public void verifyPostAPI() {        // Given
        given()
                .filter(new AllureRestAssured()) //设置 AllureRestAssured 过滤器，用来在测试报告中展示请求和响应信息
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .body("{\"title\": \"foo\", \"body\": \"bar\", \"userId\": 1\n}")
                .post("/posts")

                // Then
                .then()
                .statusCode(201)
                // To verify correct value
                .body("userId", equalTo(1))
                .body("id", equalTo(101))
                .body("title", equalTo("foo"))
                .body("body", equalTo("bar"));
    }

}
```

- 运行测试并生成 Allure 报告

```bash
gradle clean test 
```

> 生成的 Allure 报告在项目根目录的 build/allure-results 文件下

- 预览 Allure 报告

```bash
gradle allureServe
```

> 运行命令会自动打开浏览器，预览 Allure 报告

![allure-report](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/JsHrOQ.png)

![allure-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/ZXgnOD.png)

## 参考资料

- Rest assured 官方文档：<https://rest-assured.io/>

- Rest assured 官方 github：<https://github.com/rest-assured/rest-assured>

- Rest assured 官方文档中文翻译：<https://github.com/RookieTester/rest-assured-doc>
