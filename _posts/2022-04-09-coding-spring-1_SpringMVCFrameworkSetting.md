---
title: Spring Web MVC framework Setting
layout: post
categories: coding
tags: spring
---
## MVC
Model - View - Controller는 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 소프트웨어 디자인 패턴이다.    
- Model: 핵심 기능과 데이터 보관 (Business Logic)
- View: 사용자에게 정보 표시 (레이아웃과 화면)
- Controller: 사용자로부터 요청을 입력받아 처리

각 부분이 별도의 컴포넌트로 분리되어 있어서 서로 영향을 받지 않고 개발 작업을 수행할 수 있다.

## Spring MVC를 위한 필수 설정
### 1. Maven Configuration (pom.xml)    
라이브러리 의존성 추가    

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.mohyerolo</groupId>
	<artifactId>Example</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<name>Example</name>
	<!-- FIXME change it to the project's website -->
	<url>http://www.example.com</url>
	<description>...<description>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<maven.compiler.source>11</maven.compiler.source>
		<maven.compiler.target>11</maven.compiler.target>
		<java.version>11</java.version>
		<spring.version>5.2.4.RELEASE</spring.version>
        ...
	</properties>

	<dependencies>
		<!-- Spring Framework Project libraries -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>${spring.version}</version>
		</dependency>
        ...
	</dependencies>

	<build>
		<finalName>Example</finalName>
		<pluginManagement>
			<plugins>
				<plugin>
					<artifactId>maven-clean-plugin</artifactId>
					<version>3.1.0</version>
				</plugin>
                ...
			</plugins>
		</pluginManagement>
	</build>
</project>
```

### 2. Web Deployment Descriptor (web.xml)    
Deploy할 때 Servlet의 정보를 설정해준다.    
구체적인 설정 내용: DispatcherServlet, ContextLoaderListener, Filter    
__servlet-mapping__ 의 url-pattern : 웹 어플리케이션이 실행될 때, url에 아무 요청이 없다면 appServlet이 실행된다.    
__servlet__ 의 param-value: Spring MVC의 servlet 설정을 지정    
__context-param__ : 프로젝트 수행 시 사용할 Bean들을 정의하는 파일 지정    
__listener__ : 리스너 지정    
__filter__ 의 filter-name: 파라미터 인코딩 필터 설정    

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns="http://xmlns.jcp.org/xml/ns/javaee" 
xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
				 id="WebApp_ID" version="4.0">
  <display-name>Example</display-name>
  
  <context-param>
    <param-name>log4jConfigLocation</param-name>
    <param-value>classpath:log4j.properties</param-value>
  </context-param>
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>
       	classpath:applicationContext.xml
      	classpath:dataAccessContext-mybatis.xml 
	</param-value>
  </context-param>
  
  <!-- 요청 정보를 분석해서 컨트롤러를 선택하는 서블릿을 지정 -->
   <servlet>
    <servlet-name>appServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <!-- 현재 웹 애플리케이션에서 받아들이는 모든 요청에 대해 appServlet이라는 이름으로 정의되어 있는 서블릿을 사용 -->
  <servlet-mapping>
    <servlet-name>appServlet</servlet-name>
    <!-- <url-pattern>*.do</url-pattern> -->
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  
  <!-- 리스너 설정 (BeanFactory 지정) -->
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  
  <!-- 파라미터 인코딩 필터 설정 - 한글 처리 코드 -->
  <filter>
  	<filter-name>encodingFilter</filter-name>
  	<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>
  	</init-param>
  	<init-param>
  		<param-name>forceEncoding</param-name>
  		<param-value>true</param-value>
  	</init-param>
  </filter>
  
  <!-- 위에 지정한 encodingFilter 이름을 모든 패턴에 적용 -->
  <filter-mapping>
  	<filter-name>encodingFilter</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
  
  <welcome-file-list>
    <welcome-file>index.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```

### 3. Spring MVC Configuration Files    
    dispatcher-servlet.xml, applicatonContext.xml, service-context.xml, dao-context.xml, security-context.xml

### References
- <https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html>
