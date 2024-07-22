---
layout: single
title: "Spring setting - xml"
categories: spring
tag: [spring, setting, xml]
toc: true
author_profile: false
sidebar:
    nav: "docs"
published: false
---

# tomcat - web.xml
이클립스에서 tomcat을 서버로 설정  
Servers에서 `web.xml`  
아래에서 기본적으로 설정된 DefaultServlet을 확인할 수 있다.
```xml
<servlet>
    <servlet-name>default</servlet-name>
    <servlet-class>org.apache.catalina.servlets.DefaultServlet</servlet-class>
    <init-param>
        <param-name>debug</param-name>
        <param-value>0</param-value>
    </init-param>
    <init-param>
        <param-name>listings</param-name>
        <param-value>false</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
```

# spring - web.xml
Spring Project에서 src/main/webapp/WEB-INF/경로에  
`web.xml`을 추가
`DispatcherServlet` 설정과  
`servlet-context.xml`, `root-context.xml` 등의 경로 설정과 같은  
프로젝트 전반의 설정을 한다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="4.0"
	xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee                       
						http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd">

	<!-- 현재 웹 애플리케이션에서 받아들이는 모든 요청에 대해 appServlet이라는 이름으로 정의되어 있는 서블릿을 사용하겠다. -->
	<servlet-mapping>
		<servlet-name>appServlet</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
	<!-- 요청 정보를 분석해서 컨트롤러를 선택하는 서블릿을 지정한다. -->
	<servlet>
        <servlet-name>appServlet</servlet-name>
        <!-- Spring MVC에서 제공하고 있는 기본 서블릿을 지정한다. -->
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- Spring MVC 설정을 위한 xml 파일을 지정한다. -->
        <init-param>
        	<param-name>contextConfigLocation</param-name>
        	<param-value>/WEB-INF/config/servlet-context.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <!-- Bean을 정의할 xml 파일을 지정한다. -->
    <context-param>
    	<param-name>contextConfigLocation</param-name>
    	<param-value>/WEB-INF/config/root-context.xml</param-value>
    </context-param>
    
    <!-- 리스너설정 -->
    <listener>
    	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    
    <!-- 파라미터 인코딩 필터 설정 -->
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
    
    <filter-mapping>
    	<filter-name>encodingFilter</filter-name>
    	<url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
```

# spring - root-context.xml
프로젝트 수행 시 Bean 사용을 위한 .xml파일
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xsi:schemaLocation="http://www.springframework.org/schema/beans
	   					   http://www.springframework.org/schema/beans/spring-beans.xsd">
	    <!-- 사용하고자 하는 bean이 존재하면 이 파일에 추가하면 된다 -->
</beans>
```

# spring - servlet-context.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="http://www.springframework.org/schema/mvc"
			 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			 xmlns:beans="http://www.springframework.org/schema/beans"
			 xmlns:context="http://www.springframework.org/schema/context"
			 xsi:schemaLocation="http://www.springframework.org/schema/mvc
			 					 http://www.springframework.org/schema/mvc/spring-mvc.xsd
			 					 http://www.springframework.org/schema/beans
			 					 http://www.springframework.org/schema/beans/spring-beans.xsd
			 					 http://www.springframework.org/schema/context
			 					 http://www.springframework.org/schema/context/spring-context.xsd">
			 					 
	<!-- 스캔한 패지키 내부의 클래스 중 Controller 어노테이션을 가지고 있는 클래스들을 Controller로 로딩하도록 한다 -->
	<annotation-driven/>
	
	<!-- 스캔할 bean들이 모여있는 패키지를 지정한다. -->
	<context:component-scan base-package="kr.co.softcampus.controller"/>
	
	<!-- Controller의 메서드에서 반환하는 문자열 앞 뒤에 붙힐 경로 정보를 셋팅한다. -->
	<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/"/>
		<beans:property name="suffix" value=".jsp"/>
	</beans:bean>
	
	<!-- 정적파일(이미지, 사운드, 동영상, JS, CSS 등등) 경로 셋팅 -->
	<resources mapping="/**" location="/resources/"/>
	
			 
</beans:beans>
```

> 출처 :  [인프런 - 윤재성의 만들면서 배우는 Spring MVC 5](https://www.inflearn.com/course/spring-mvc5-project)

