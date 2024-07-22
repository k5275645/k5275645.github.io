---
layout: single
title: "Spring setting - porm.xml"
categories: spring
tag: [spring, setting]
toc: true
author_profile: false
sidebar:
    nav: "docs"
published: false
---

# spring porm.xml
## https://mvnrepository.com/
- 링크 [mvnrepository](https://mvnrepository.com/)
- 위 주소에서 porm.xml의 dependency 세팅을 위한 정보를 찾을 수 있다.

## 기본 세팅
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>SpringMVCStep1</groupId>
	<artifactId>SpringMVCStep1</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>
	<build>
		<plugins>
			<plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.8.1</version>
				<configuration>
					<release>16</release>
				</configuration>
			</plugin>
			<plugin>
				<artifactId>maven-war-plugin</artifactId>
				<version>3.2.3</version>
			</plugin>
		</plugins>
	</build>

	<!-- 라이브러리 버전관리 -->
	<properties>
		<javax.servlet-version>4.0.1</javax.servlet-version>
		<javax.servlet.jsp-version>2.3.3</javax.servlet.jsp-version>
		<javax.servlet.jsp.jstl-version>1.2</javax.servlet.jsp.jstl-version>
		<org.springframework-version>5.3.13</org.springframework-version>
		<!-- <org.springframework-version>4.3.30.RELEASE</org.springframework-version> -->
	</properties>

	<!-- 라이브러리 셋팅 -->
	<dependencies>
		<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>${javax.servlet-version}</version>
			<scope>provided</scope>
		</dependency>
		<!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
		<dependency>
			<groupId>javax.servlet.jsp</groupId>
			<artifactId>javax.servlet.jsp-api</artifactId>
			<version>${javax.servlet.jsp-version}</version>
			<scope>provided</scope>
		</dependency>
		<!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>${javax.servlet.jsp.jstl-version}</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
	</dependencies>

</project>
```

> 출처 :  [인프런 - 윤재성의 만들면서 배우는 Spring MVC 5](https://www.inflearn.com/course/spring-mvc5-project)