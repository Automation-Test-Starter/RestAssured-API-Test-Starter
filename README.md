
# RestAssured 接口自动化测试开始启动项目

关于使用 RestAssured 进行 API 测试的快速启动项目介绍文档。

**中文** | [English](/README_EN.md)

- [RestAssured 接口自动化测试开始启动项目](#restassured-接口自动化测试开始启动项目)
  - [RestAssured 介绍](#restassured-介绍)
  - [项目结构](#项目结构)
    - [Gradle 构建的版本](#gradle-构建的版本)
    - [Maven 构建的版本](#maven-构建的版本)
  - [项目依赖](#项目依赖)
  - [项目初始化](#项目初始化)
    - [Gradle 版本](#gradle-版本)
      - [创建一个空的 Gradle 工程](#创建一个空的-gradle-工程)
      - [配置项目 build.gradle](#配置项目-buildgradle)
      - [gradle build 项目并初始化](#gradle-build-项目并初始化)
      - [初始化目录](#初始化目录)
      - [编写脚本](#编写脚本)
      - [调试脚本](#调试脚本)
    - [Maven 版本](#maven-版本)
      - [创建一个空的 Maven 工程](#创建一个空的-maven-工程)
      - [配置项目 pom.xml](#配置项目-pomxml)
      - [初始化目录](#初始化目录-1)
      - [编写脚本](#编写脚本-1)
      - [调试脚本](#调试脚本-1)

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
- Gradle 6.0+ 或 Maven 3.0+，我使用的 Gradle 8.44,，我使用的 Gradle 8.44 和 Maven 3.9.5
- RestAssured 4.3.3+

## 项目初始化

### Gradle 版本

#### 创建一个空的 Gradle 工程

#### 配置项目 build.gradle

#### gradle build 项目并初始化

#### 初始化目录

#### 编写脚本

#### 调试脚本

### Maven 版本

#### 创建一个空的 Maven 工程

#### 配置项目 pom.xml

#### 初始化目录

#### 编写脚本

#### 调试脚本
