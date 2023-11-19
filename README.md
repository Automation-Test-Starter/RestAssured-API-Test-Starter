<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->
<div align="right"><strong><a href="./README_ZH.md">🇨🇳中文</a></strong>  | <strong>🇬🇧English</strong></div>
<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->

# RestAssured-API-Test-Starter

Introductory documentation for a quick-start project on API testing with RestAssured.

- [RestAssured-API-Test-Starter](#restassured-api-test-starter)
  - [Introduction of RestAssured](#introduction-of-restassured)
  - [Project structure](#project-structure)
    - [Gradle-built versions](#gradle-built-versions)
    - [Maven-built versions](#maven-built-versions)
  - [Project dependency](#project-dependency)
  - [Building a REST Assured API test project from 0 to 1](#building-a-rest-assured-api-test-project-from-0-to-1)
    - [Gradle version](#gradle-version)
      - [Initialize an empty Gradle project](#initialize-an-empty-gradle-project)
      - [Configuration build.gradle](#configuration-buildgradle)
      - [testng.xml configuration](#testngxml-configuration)
      - [gradle build project and initialize](#gradle-build-project-and-initialize)
      - [initialization project directory](#initialization-project-directory)
      - [Introduction of demo test API](#introduction-of-demo-test-api)
        - [Get API](#get-api)
        - [Post API](#post-api)
      - [Writing Test cases](#writing-test-cases)
      - [Debugging test cases](#debugging-test-cases)
      - [Viewing Test Reports](#viewing-test-reports)
        - [Command Line Report](#command-line-report)
        - [testng html Report](#testng-html-report)
    - [Maven version](#maven-version)
      - [Initialize an empty Maven project](#initialize-an-empty-maven-project)
      - [Configuration pom.xml](#configuration-pomxml)
      - [Configuration testng.xml](#configuration-testngxml)
      - [initialization maven project directory](#initialization-maven-project-directory)
      - [The api used by Demo](#the-api-used-by-demo)
      - [Writing Test cases](#writing-test-cases-1)
      - [Debugging test cases](#debugging-test-cases-1)
      - [Viewing Test Reports](#viewing-test-reports-1)
        - [terminal report](#terminal-report)
        - [testng html report](#testng-html-report-1)
  - [Advanced Usage](#advanced-usage)
    - [Verifying Response Data](#verifying-response-data)
      - [response body assertion](#response-body-assertion)
        - [json assertion](#json-assertion)
        - [XML assertion](#xml-assertion)
      - [Cookie assertion](#cookie-assertion)
      - [Status Code Assertion](#status-code-assertion)
      - [Header Assertion](#header-assertion)
      - [Content-Type Assertion](#content-type-assertion)
      - [Full body/content matching Assertion](#full-bodycontent-matching-assertion)
      - [Measuring Response Time](#measuring-response-time)
    - [File Upload](#file-upload)
    - [Logging](#logging)
      - [Global logging configuration](#global-logging-configuration)
        - [Steps to add global logging configuration](#steps-to-add-global-logging-configuration)
        - [Global Logging Code Example](#global-logging-code-example)
        - [Viewing Global Log Output](#viewing-global-log-output)
      - [Localized logging configuration](#localized-logging-configuration)
        - [Steps to add Localized logging configuration](#steps-to-add-localized-logging-configuration)
        - [Viewing Localized Log Output](#viewing-localized-log-output)
      - [LogConfig Configuration Description](#logconfig-configuration-description)
      - [Request Logging](#request-logging)
      - [Response Logging](#response-logging)
      - [Log if validation fails](#log-if-validation-fails)
      - [Header Blacklist Configuration](#header-blacklist-configuration)
    - [Filters](#filters)
      - [Ordered Filters](#ordered-filters)
      - [Response Builder](#response-builder)
    - [CI/CD integration](#cicd-integration)
      - [integration github action](#integration-github-action)
        - [The Gradle version integration github action](#the-gradle-version-integration-github-action)
        - [The Maven version integration github action](#the-maven-version-integration-github-action)
    - [Integrating allure test reports](#integrating-allure-test-reports)
      - [allure Introduction](#allure-introduction)
      - [Integration steps](#integration-steps)
        - [The Maven version integration of allure](#the-maven-version-integration-of-allure)
        - [The Gradle version of allure integration](#the-gradle-version-of-allure-integration)
  - [Reference](#reference)

## Introduction of RestAssured

REST Assured is a Java testing framework for testing RESTful APIs that enables developers/testers to easily write and execute API tests. It is designed to make API testing simple and intuitive, while providing rich functionality and flexibility. The following are some of the key features and uses of REST Assured:

1. Initiating HTTP requests: REST Assured allows you to easily build and initiate HTTP GET, POST, PUT, DELETE and other types of requests. You can specify the request's URL, headers, parameters, body, and other information.

2. Chained Syntax: REST Assured uses chained syntax to make test code more readable and easy to write. You can describe your test cases in a natural way without writing tons of code.

3. Assertions and Checksums: REST Assured provides a rich set of checksums that can be used to validate API response status codes, response bodies, response headers, and so on. You can add multiple assertions according to your testing needs.

4. Support for multiple data formats: REST Assured supports a variety of data formats, including JSON, XML, HTML, Text and so on. You can use appropriate methods to handle different formats of response data.

5. Integration with BDD (Behavior-Driven Development): REST Assured can be used in conjunction with BDD frameworks (such as Cucumber), allowing you to better describe and manage test cases.

6. Simulate HTTP Server: REST Assured also includes a simulation of an HTTP server, allowing you to simulate the behavior of an API for end-to-end testing.

7. Extensibility: REST Assured can be customized with plug-ins and extensions to meet specific testing needs.

Overall, REST Assured is a powerful and easy-to-use API testing framework that helps you easily perform RESTful API testing and provides many tools to verify the correctness and performance of an API. Whether you are a beginner or an experienced developer/tester, REST Assured is a valuable tool for quickly getting started with API automation testing.

## Project structure

### Gradle-built versions

```text
- src
  - main
    - java
      - (The main source code of the application)
  - test
    - test
      - api
        - (REST Assured test code)
          - UsersAPITest.java
          - ProductsAPITest.java
        - TestConfig.java
          - TestConfig.java
    - resources
      - (configuration files, test data, etc.)
  - (other project files and resources)
- build.gradle (Gradle project configuration file)
```

In this example directory structure:

- src/test/java/api directory is used to hold REST Assured test classes, each of which typically involves tests for one or more related API endpoints. For example, UsersAPITest.java and ProductsAPITest.java could contain tests for user management and product management.
- The src/test/java/util directory can be used to store tool classes that are shared among tests, such as TestConfig.java for configuring REST Assured.
- The src/test/resources directory can contain test data files, configuration files, and other resources that can be used in tests.
- build.gradle is the gradle project's configuration file, which is used to define the project's dependencies, build configuration, and other project settings.

### Maven-built versions

```text
- src
  - main
    - java
      - (The main source code of the application)
  - test
    - java
      - api
        - (REST Assured test code)
          - UsersAPITest.java
          - ProductsAPITest.java
        - util
          - TestConfig.java
    - resources
      - (configuration files, test data, etc.)
  - (other project files and resources)
- pom.xml (Maven project configuration file)
```

In this example directory structure:

- src/test/java/api directory is used to hold REST Assured test classes, each of which typically involves tests for one or more related API endpoints. For example, UsersAPITest.java and ProductsAPITest.java could contain tests for user management and product management.
- The src/test/java/util directory can be used to store tool classes that are shared among tests, such as TestConfig.java for configuring REST Assured.
- The src/test/resources directory can contain test data files, configuration files, and other resources that can be used in the tests.
- pom.xml is a Maven project configuration file that is used to define project dependencies, build configurations, and other project settings.

## Project dependency

- JDK 1.8+, I'm using JDK 19
- Gradle 6.0+ or Maven 3.0+, I'm using Gradle 8.44 and Maven 3.9.5
- RestAssured 4.3.3+, I'm using the latest version 5.3.2

## Building a REST Assured API test project from 0 to 1

REST Assured supports both Gradle and Maven build tools, you can choose one of them according to your preference. Below is a description of the initialization process for Gradle and Maven build tools.

This project is built using Gradle 8.44 and Maven 3.9.5, if you are using other versions, it may be different.

### Gradle version

See the demo project at <https://github.com/Automation-Test-Starter/RestAssured-gradle-demo>.

#### Initialize an empty Gradle project

```bash
mkdir RestAssured-gradle-demo
cd RestAssured-gradle-demo
gradle init
```

#### Configuration build.gradle

The demo project introduces the testNG testing framework. For reference only.

- Create a build.gradle file in the project root directory to configure the project.
- For reference, the following is a sample configuration

```groovy
// plugins configuration
plugins {
    id 'java' // use java plugin
}

// repositories configuration
repositories {
  mavenCentral() // user maven central repository
}

// dependencies configuration
dependencies {
    testImplementation 'io.rest-assured:rest-assured:5.3.1' // add rest-assured dependency
    testImplementation 'org.testng:testng:7.8.0' // add testng testing framework dependency
    implementation 'org.uncommons:reportng:1.1.4' // add testng reportng dependency
    implementation 'org.slf4j:slf4j-api:2.0.9' // add slf4j dependency for test logging
    implementation 'org.slf4j:slf4j-simple:2.0.9' // add slf4j dependency for test logging
    implementation group: 'com.google.inject', name: 'guice', version: '7.0.0'
}

// test configuration
test {
    reports.html.required = false // set gradle html report to false
    reports.junitXml.required = false // set gradle junitXml report to false
    // use testng testing framework
    useTestNG() {
        useDefaultListeners = true
        suites 'src/test/resources/testng.xml' // set testng.xml file path
    }
    testLogging.showStandardStreams = true // output test log to console
    testLogging.events "passed", "skipped", "failed" // deny output test log to console
}
```

> You can copy the contents of the build.gradle file in this project. For more configuration refer to [Official Documentation](https://github.com/rest-assured/rest-assured/wiki/GettingStarted#rest-assured)

#### testng.xml configuration

- Create a resources directory under the src/test directory to store test configuration files.

- Create a testng.xml file in the resources directory to configure the TestNG test framework.

- For reference, the following is a sample configuration

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="restAssured-gradleTestSuite">
<test thread-count="1" name="Demo">
    <classes>
        <class name="com.example.TestDemo"/> <!-- test case class-->
    </classes>
</test> <!-- Test -->
</suite> <!-- Suite -->
```

#### gradle build project and initialize

- Open the Terminal window of the project with an editor and execute the following command to confirm that the project build was successful

```bash
gradle build
```

- Initialization complete: After completing the wizard, Gradle will generate a basic Gradle project structure in the project directory
  
#### initialization project directory

The directory structure can be found in >> [Project structure](#project-structure)

Create a new test class in the project's test source directory. By default, Gradle usually places the test source code in the src/test/java directory. You can create a package of test classes in that directory and create a new test class in the package

To create a test class for TestDemo, you can create files with the following structure
  
```text
src
└── test
    └── java
        └── com
            └── example
                └── TestDemo.java
```

#### Introduction of demo test API

##### Get API

- HOST: https://jsonplaceholder.typicode.com
- API path: /posts/1
- Request method: GET
- Request Parameters: None
- Request header: "Content-Type": "application/json; charset=utf-8"
- Request Body: None
- Response status code: 200
- Response header: "Content-Type": "application/json; charset=utf-8"
- Response body:

```json
{
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

##### Post API

- HOST: https://jsonplaceholder.typicode.com
- API path:/posts
- Request method: POST
- Request Parameters: None
- Request header:"Content-Type": "application/json; charset=utf-8"
- Request Body:raw json format
- Request Body:

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
```

- Response status code: 201
- Response header:"Content-Type": "application/json; charset=utf-8"
- Response body:

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1,
    "id": 101
}
```

#### Writing Test cases

- Open the TestDemo.java file and start writing the test script.

- The example script is as follows. For reference

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

#### Debugging test cases

- Open the Terminal window for this project and run the test script by executing the following command

```bash
gradle test
```

#### Viewing Test Reports

##### Command Line Report

![gradle-test-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/gradle-report1.png)

##### testng html Report

- Open the project build/reports/tests/test directory.
- Click on the index.html file to view the test report.

![gradle-test-report2](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/gradle-report2.png)

### Maven version

See the demo project at <https://github.com/Automation-Test-Starter/RestAssured-maven-demo>

#### Initialize an empty Maven project

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=RestAssured-maven-demo -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Initialization complete: After completing the wizard, Maven will create a new project directory and a basic Maven project structure

#### Configuration pom.xml

Add the following to the pom.xml file in your project

> You can copy the contents of the pom.xml file in this project. For more information on configuration, please refer to the [official documentation](https://github.com/rest-assured/rest-assured/wiki/GettingStarted#rest-assured).

```xml
<!-- dependencies config -->
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
  <!-- plugin config -->
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

#### Configuration testng.xml

- Create a resources directory under the src/test directory to store test configuration files.

- Create a testng.xml file in the resources directory to configure the TestNG test framework.

- For reference, the following is a sample configuration

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="restAssured-gradleTestSuite">
<test thread-count="1" name="Demo">
    <classes>
        <class name="com.example.TestDemo"/> <!-- test case class-->
    </classes>
</test> <!-- Test -->
</suite> <!-- Suite -->
```

#### initialization maven project directory

The directory structure can be found in >> [Project structure](#project-structure)

Create a new test class in the project's test source directory. By default, Gradle usually places the test source code in the src/test/java directory. You can create a package of test classes in that directory and create a new test class in the package

To create a test class for TestDemo, you can create files with the following structure
  
```text
src
└── test
    └── java
        └── com
            └── example
                └── TestDemo.java
```

#### The api used by Demo

referable to >> [Introduction of demo test API](#introduction-of-demo-test-api)

#### Writing Test cases

- Open the TestDemo.java file and start writing the test script.

- The example script is as follows. For reference

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

#### Debugging test cases

- Open the Terminal window for this project and run the test script by executing the following command

```bash
mvn test
```

#### Viewing Test Reports

##### terminal report

![maven-test-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/maven-report1.png)

##### testng html report

- Open the project target/surefire-reports directory.
- Click on the index.html file to view the test report.

![maven-test-report2](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/maven-report2.png)

## Advanced Usage

### Verifying Response Data

You can verify Response status code, Response status line, Response cookies, Response headers, Response content type and Response body.

#### response body assertion

##### json assertion
  
Assume that the GET request (to <http://localhost:8080/lotto>) returns JSON as:

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

REST assured makes it easy to make get requests and process response messages.

- Asserts whether the value of lottoId is equal to 5. For example:

```java
get("/lotto").then().body("lotto.lottoId", equalTo(5));
```

- Assertion The values for winnerId include 23 and 54. For example:

```java
get("/lotto").then().body("lotto.winners.winnerId", hasItems(23, 54));
```

> Note: `equalTo` and `hasItems` are Hamcrest matchers which you should statically import from `org.hamcrest.Matchers`.

##### XML assertion

XML can be verified in a similar way. Imagine that a POST request to <http://localhost:8080/greetXML> returns:

```xml
<greeting>
   <firstName>{params("firstName")}</firstName>
   <lastName>{params("lastName")}</lastName>
</greeting>
```

- Asserts whether the firstName is returned correctly. For example:

```java
given().
         parameters("firstName", "John", "lastName", "Doe").
when().
         post("/greetXML").
then().
         body("greeting.firstName", equalTo("John")).
```

- Assert that firstname and lastname are returned correctly. For example:

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

#### Cookie assertion

- Asserts whether the value of the cookie is equal to cookieValue. For example:

```java
get("/x").then().assertThat().cookie("cookieName", "cookieValue")
```

- Asserts whether the value of multiple cookies is equal to the cookieValue at the same time. For example:

```java
get("/x").then().assertThat().cookies("cookieName1", "cookieValue1", "cookieName2", "cookieValue2")
```

- Asserts whether the value of the cookie contains a cookieValue. For example:

```java
get("/x").then().assertThat().cookies("cookieName1", "cookieValue1", "cookieName2", containsString("Value2"))
```

#### Status Code Assertion

- Assertion Whether the status code is equal to 200. For example:

```java
get("/x").then().assertThat().statusCode(200)
```

- Assertion Whether the status line is something. For example:

```java
get("/x").then().assertThat().statusLine("something")
```

- Assertion Whether the status line contains some. For example:

```java
get("/x").then().assertThat().statusLine(containsString("some"))
```

#### Header Assertion

- Asserts whether the value of Header is equal to HeaderValue. For example:

```java
get("/x").then().assertThat().header("headerName", "headerValue")
```

- Asserts whether the value of multiple Headers is equal to HeaderValue at the same time. For example:

```java
get("/x").then().assertThat().headers("headerName1", "headerValue1", "headerName2", "headerValue2")
```

- Asserts whether the value of the Header contains a HeaderValue. For example:

```java
get("/x").then().assertThat().headers("headerName1", "headerValue1", "headerName2", containsString("Value2"))
```

- Assert that the "Content-Length" of the Header is less than 1000. For example:

> The header can be first converted to int using the mapping function, and then asserted using the "integer" matcher before validation with Hamcrest:

```java
get("/something").then().assertThat().header("Content-Length", Integer::parseInt, lessThan(1000));
```

#### Content-Type Assertion

- Asserts whether the value of Content-Type is equal to application/json. For example:

```java
get("/x").then().assertThat().contentType(ContentType.JSON)
```

#### Full body/content matching Assertion

- Assertion Whether the response body is exactly equal to something. For example:

```java
get("/x").then().assertThat().body(equalTo("something"))
```

#### Measuring Response Time

> As of version 2.8.0 REST Assured has support measuring response time. For example:

```java
long timeInMs = get("/lotto").time()
```

or using a specific time unit:

```java
long timeInSeconds = get("/lotto").timeIn(SECONDS);

```

where 'SECONDS' is just a standard 'TimeUnit'. You can also validate it using the validation DSL:

```java
when().
      get("/lotto").
then().
      time(lessThan(2000L)); // Milliseconds
```

or

```java
when().
      get("/lotto").
then().
      time(lessThan(2L), SECONDS);
```

Note that you can only referentially correlate these measurements to server request processing times (as response times will include HTTP roundtrips, REST Assured processing times, etc., and cannot be very accurate).

### File Upload

Often we use the multipart form data technique when transferring large amounts of data to the server, such as files.
rest-assured provides a `multiPart` method to recognize whether this is a file, a binary sequence, an input stream, or uploaded text.

- Upload only one file in the form. For example:

```java
given().
        multiPart(new File("/path/to/file")).
when().
        post("/upload");
```

- Uploading a file in the presence of a control name. For example:

```java
given().
        multiPart("controlName", new File("/path/to/file")).
when().
        post("/upload");
```

- Multiple "multi-parts" entities in the same request. For example:

```java
byte[] someData = ..
given().
        multiPart("controlName1", new File("/path/to/file")).
        multiPart("controlName2", "my_file_name.txt", someData).
        multiPart("controlName3", someJavaObject, "application/json").
when().
        post("/upload");
```

- MultiPartSpecBuilder use cases. For example:

> For more usage references[MultiPartSpecBuilder](http://static.javadoc.io/io.rest-assured/rest-assured/3.0.1/io/restassured/builder/MultiPartSpecBuilder.html)：

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

- MultiPartConfig use cases. For example:

>[MultiPartConfig](http://static.javadoc.io/io.rest-assured/rest-assured/3.0.1/io/restassured/config/MultiPartConfig.html)You can specify the default control name and file name.

```java
given().config(config().multiPartConfig(multiPartConfig().defaultControlName("something-else")))  
```

> By default, the control name is configured as "something-else" instead of "file".
> For more usage references [blog introduction](http://blog.jayway.com/2011/09/15/multipart-form-data-file-uploading-made-simple-with-rest-assured/)

### Logging

When we are writing interface test scripts, we may need to print some logs during the test process so that we can view the request and response information of the interface and some other information during the test process.RestAssured provides some methods to print logs.

- RestAssured provides a global logging configuration method that allows you to configure logging before the test starts and then print the logs during the test. This method is applicable to all test cases, but it can only print request and response information, not other information.

- RestAssured also provides a localized log configuration method that prints logs during the test. This method prints request and response information as well as other information.

#### Global logging configuration

##### Steps to add global logging configuration

- Importing logging-related dependency classes
  
```java
import io.restassured.config.LogConfig;
import io.restassured.filter.log.LogDetail;
import io.restassured.filter.log.RequestLoggingFilter;
import io.restassured.filter.log.ResponseLoggingFilter;
```

- Adding logging configuration to the setup() method

> Use LogConfig configuration to enable logging of requests and responses, as well as to enable nice output formatting. Enabled logging filters for requests and responses, which will log details of requests and responses.

```java
// Setting the Global Request and Response Logging Configuration
        RestAssured.config = RestAssured.config()
                .logConfig(LogConfig.logConfig()
                        .enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
                        .enablePrettyPrinting(true));
```

- Enabled global logging filters in the setup() method

```java
// Enable global request and response logging filters
    RestAssured.filters(new RequestLoggingFilter(), new ResponseLoggingFilter());
```

##### Global Logging Code Example

```java
package com.example;

import io.restassured.RestAssured;
// Importing logging-related dependency classes
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
        // Setting the Global Request and Response Logging Configuration
        RestAssured.config = RestAssured.config()
                .logConfig(LogConfig.logConfig()
                        .enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
                        .enablePrettyPrinting(true));
        // Enable global request and response logging filters
        RestAssured.filters(new RequestLoggingFilter(), new ResponseLoggingFilter());
    }

    @Test(description = "Verify that the Get Post API returns correctly")
    public void verifyGetAPI() {
      // Test cases have been omitted, refer to the demo
    }

    @Test(description = "Verify that the publish post API returns correctly")
    public void verifyPostAPI() {
      // Test cases have been omitted, refer to the demo
    }
}
```

##### Viewing Global Log Output

- Open the Terminal window for this project and run the test script by executing the following command
- Viewing Log Output

![log-sceenshot1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/9Mh9Z8.png)

#### Localized logging configuration

In RestAssured, you can make localized logging configurations to enable or disable logging for specific test methods or requests without affecting the global configuration.

##### Steps to add Localized logging configuration

- Add logging configuration is enabled in the test method for which you want to print logs

```java
    @Test(description = "Verify that the Get Post API returns correctly")
    public void verifyGetAPI() {

        // Given
        given()
                .log().everything(true)  // Output request-related logs
                .baseUri("https://jsonplaceholder.typicode.com")
                .header("Content-Type", "application/json")

                // When
                .when()
                .get("/posts/1")

                // Then
                .then()
                .log().everything(true)  // Output response-related logs
                .statusCode(200)
    }
```

##### Viewing Localized Log Output

- Open the Terminal window for this project and run the test script by executing the following command
- Viewing Log Output

![report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/GxZyyG.png)

#### LogConfig Configuration Description

In Rest-Assured, you can use the `LogConfig` class to configure logging of requests and responses. The `LogConfig` allows you to define the level of logging detail, the output format, the location of the output, and so on. The following are some common `LogConfig` configuration examples:

1. **Enable logging of requests and responses:**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL));;
   ```

   This will enable logging of requests and responses only if validation fails.

2. **Configure the output level:**

   ``` java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.HEADERS));;
   ```

   This will log only the request and response headers.

3. **Configure the location of the output:**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
           .enablePrettyPrinting(true)
           .defaultStream(FileOutputStream("log.txt"))); ;enablePrettyPrinting(true).enablePrettyPrinting(true)
   ```

   This outputs the log records to a file named "log.txt".

4. **Configure the nice output format:**

   ```java
   RestAssured.config = RestAssured.config()
       .logConfig(LogConfig.logConfig().enableLoggingOfRequestAndResponseIfValidationFails(LogDetail.ALL)
           .enablePrettyPrinting(true));
   ```

   This will enable nice output formatting and make the logs easier to read.

You can combine these configuration options according to your specific needs and set it to `RestAssured.config` to configure global request and response logging. This will help log and review requests and responses in RestAssured for debugging and analyzing issues.

#### Request Logging

Starting with version 1.5, REST Assured supports logging request specifications before they are sent to the server using RequestLoggingFilter. Note that HTTP Builder and HTTP Client may add headers other than what is printed in the log. The filter will only log the details specified in the request specification. That is, you cannot consider the details logged by the RequestLoggingFilter to be the details actually sent to the server. In addition, subsequent filters may change the request after logging has occurred. If you need to log what is actually sent over the network, see the HTTP Client Logging documentation or use an external tool such as fiddler.

Examples：

```java
given().log().all() // Log all request specification details including parameters, headers and body
given().log().params() // Log only the parameters of the request
given().log().body() // Log only the request body
given().log().headers()  // Log only the request headers
given().log().cookies()  // Log only the request cookies
given().log().method()  // Log only the request method
given().log().path()  // Log only the request path
```

#### Response Logging

- Wanting to print only the body of the response, regardless of the status code, you can do the following.
, for example:

```java
get("/x").then().log().body()
```

- The response body will be printed whether or not an error occurs. If only interested in printing the response body when an error occurs, for example:

```java
get("/x").then().log().ifError()
```

- Record all details in the response, including status lines, headers, and cookies, for example:

```java
get("/x").then().log().all()   
```

- Record only the status line, header, or cookie in the response, for example:

```java
get("/x").then().log().statusLine()  // Only log the status line
get("/x").then().log().headers()  // Only log the response headers
get("/x").then().log().cookies()   // Only log the response cookies
```

- Configured to log a response only when the status code matches a value. for example:

```java
get("/x").then().log().ifStatusCodeIsEqualTo(302)   // Only log if the status code is equal to 302
get("/x").then().log().ifStatusCodeMatches(matcher)   // Only log if the status code matches the supplied Hamcrest matcher
```

#### Log if validation fails

- Since REST Assured 2.3.1 you can log the request or response only if the validation fails. To log the request do. for example:

```java
given().log().ifValidationFails()
```

- To log the response. for example:

```java
then().log().ifValidationFails()
```

- It can be enabled for both requests and responses using LogConfig, for example:

```java
given().config(RestAssured.config().logConfig(logConfig().enableLoggingOfRequestAndResponseIfValidationFails(HEADERS)))
```

> If authentication fails, the log only records the request header.

- Another shortcut to enable request and response logging for all requests if authentication fails, for example:
  
```java
RestAssured.enableLoggingOfRequestAndResponseIfValidationFails();
```

- Starting with version 4.5.0, you can also use specify the message that will be displayed if the onFailMessage test fails, for example:
  
```java
when().
      get().
then().
      onFailMessage("Some specific message").
      statusCode(200);
```

#### Header Blacklist Configuration

Starting with REST Assured 4.2.0, it is possible to blacklist headers so that they do not show up in request or response logs. Instead, the header value will be replaced with [ BLACKLISTED ] . You can enable this feature on a per-header basis using LogConfig, for example:
  
```java
given().config(config().logConfig(logConfig().blacklistHeader("Accept")))  
```

### Filters

In RestAssured, you can use filters to modify requests and responses. Filters allow you to modify requests and responses at different stages of the request and response process. For example, you can modify the request before the request or the response after the response. You can use filters to add request headers, request parameters, request bodies, response headers, response bodies, and so on.

Filters can be used to implement custom authentication schemes, session management, logging, and so on. To create a filter, you need to implement the io.restassured.filter.Filter interface. To use a filter, you can do the following:

```java
given().filter(new MyFilter())  
```

There are a couple of filters provided by REST-Assured that are ready to use:

- `io.restassured.filter.log.RequestLoggingFilter`: A filter that'll print the request specification details.
- `io.restassured.filter.log.ResponseLoggingFilter`: A filter that'll print the response details if the response matches a given status code.
- `io.restassured.filter.log.ErrorLoggingFilter`: A filter that'll print the response body if an error occurred (status code is between 400 and 500).

#### Ordered Filters

As of REST Assured 3.0.2 you can implement the `io.restassured.filter.OrderedFilter` interface if you need to control the filter ordering. Here you implement the getOrder method to return an integer representing the precedence of the filter. A lower value gives higher precedence. The highest precedence you can define is Integer.MIN_VALUE and the lowest precedence is Integer.MAX_VALUE. Filters not implementing `io.restassured.filter.OrderedFilter` will have a default precedence of 1000.

[examples](https://github.com/rest-assured/rest-assured/blob/master/examples/rest-assured-itest-java/src/test/java/io/restassured/itest/java/OrderedFilterITest.java)

#### Response Builder

If you need to change the Response from a filter you can use the ResponseBuilder to create a new Response based on the original response. For example if you want to change the body of the original response to something else you can do:

```java
Response newResponse = new ResponseBuilder().clone(originalResponse).setBody("Something").build();
```

### CI/CD integration

#### integration github action

Use github action as an example, and other CI tools similarly

##### The Gradle version integration github action

See the demo at <https://github.com/Automation-Test-Starter/RestAssured-gradle-demo>

- Create the .github/workflows directory: In your GitHub repository, create a directory called .github/workflows. This will be where the GitHub Actions workflow files will be stored.

- Create a workflow file: Create a YAML-formatted workflow file, such as gradle.yml, in the .github/workflows directory.

- Edit the gradle.yml file: Copy the following into the file

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

- Commit the code: Add the gradle.yml file to your repository and commit.
- View test reports: In GitHub, navigate to your repository. Click the Actions tab at the top and then click the Gradle and REST Assured Tests workflow on the left. You should see the workflow running, wait for the execution to complete and you can view the results.

![gradle-test-report3](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/gradle-report3.png)

##### The Maven version integration github action

See the demo at <https://github.com/Automation-Test-Starter/RestAssured-maven-demo>

- Create the .github/workflows directory: In your GitHub repository, create a directory called .github/workflows. This will be where the GitHub Actions workflow files will be stored.

- Create a workflow file: Create a YAML-formatted workflow file, such as maven.yml, in the .github/workflows directory.

- Edit the maven.yml file: Copy the following into the file
  
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

- Commit the code: Add the maven.yml file to the repository and commit.
- View test reports: In GitHub, navigate to your repository. Click the Actions tab at the top and then click the Maven and REST Assured Tests workflow on the left. You should see the workflow running, wait for the execution to complete and you can view the results.

![maven-test-report3](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/maven-report3.png)

### Integrating allure test reports

#### allure Introduction

Allure is an open source testing framework for generating beautiful, interactive test reports. It can be used with a variety of testing frameworks (e.g. JUnit, TestNG, Cucumber, etc.) and a variety of programming languages (e.g. Java, Python, C#, etc.).

Allure test reports have the following features:

- Aesthetically pleasing and interactive: Allure test reports present test results in an aesthetically pleasing and interactive way, including graphs, charts and animations. This makes test reports easier to read and understand.
- Multi-language support: Allure supports multiple programming languages, so you can write tests in different languages and generate uniform test reports.
Test case level details: Allure allows you to add detailed information to each test case, including descriptions, categories, labels, attachments, historical data, and more. This information helps provide a more complete picture of the test results.
- Historical Trend Analysis: Allure supports test historical trend analysis, which allows you to view the historical performance of test cases, identify issues and improve test quality.
- Categories and Tags: You can add categories and tags to test cases to better organize and categorize test cases. This makes reporting more readable.
- Attachments and Screenshots: Allure allows you to attach files, screenshots, and other attachments to better document information during testing.
- Integration: Allure seamlessly integrates with a variety of testing frameworks and build tools (e.g. Maven, Gradle), making it easy to generate reports.
- Open Source Community Support: Allure is an open source project with an active community that provides extensive documentation and support. This makes it the tool of choice for many automated testing teams.

The main goal of Allure test reports is to provide a clear, easy-to-read way to present test results to help development teams better understand the status and quality of their tests, quickly identify problems, and take the necessary action. Whether you are a developer, tester, or project manager, Allure test reports provide you with useful information to improve software quality and reliability.

Official Website: <https://docs.qameta.io/allure/>

#### Integration steps

##### The Maven version integration of allure

- Add allure dependency in POM.xml

> Copy the contents of the pom.xml file in this project

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

- Add allure plugin to POM.xml

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

- Create test code for testing the REST API under src/test/java.

> The following is an example of a demo, see the project for details: <https://github.com/Automation-Test-Starter/RestAssured-maven-demo>.

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
                .filter(new AllureRestAssured()) // Set up the AllureRestAssured filter to display request and response information in the test report
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
                .filter(new AllureRestAssured()) // Set up the AllureRestAssured filter to display request and response information in the test report
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

- Run tests and generate Allure reports

```bash
mvn clean test
```

> The generated Allure report is in the allure-results file in the project root directory.

- Preview of the Allure Report

```bash
mvn allure:serve
```

> Running the command automatically opens a browser to preview the Allure report.

![allure-report](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/JsHrOQ.png)

![allure-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/ZXgnOD.png)

##### The Gradle version of allure integration

- Add the allure plugin to your build.gradle.

> Copy the contents of the build.gradle file in this project

```groovy
id("io.qameta.allure") version "2.11.2"
```

- Add allure dependency to build.gradle

> Copy the contents of the build.gradle file in this project

```groovy
    implementation 'io.qameta.allure:allure-testng:2.24.0' // Add allure report dependency
    implementation 'io.qameta.allure:allure-rest-assured:2.24.0' // Add allure report dependency
```

- Create test code for testing the REST API under src/test/java.

> The following is an example of a demo, see the project for details: <https://github.com/Automation-Test-Starter/RestAssured-gradle-demo>.

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
                .filter(new AllureRestAssured()) // Set up the AllureRestAssured filter to display request and response information in the test report
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
                .filter(new AllureRestAssured())                 .filter(new AllureRestAssured()) // Set up the AllureRestAssured filter to display request and response information in the test report
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

- Run the test and generate the Allure report

```bash
gradle clean test 
``

> The generated Allure report is in the build/allure-results file in the project root directory.

- Preview the Allure report

```bash
gradle allureServe
```

> Running the command automatically opens a browser to preview the Allure report.

![allure-report](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/JsHrOQ.png)

![allure-report1](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/ZXgnOD.png)

## Reference

- Rest assured official documentation: <https://rest-assured.io/>

- Rest assured official github:<https://github.com/rest-assured/rest-assured>

- Rest assured official docs in Chinese: <https://github.com/RookieTester/rest-assured-doc>
