---
layout: single
title: "Spring - getParameter"
categories: spring
tag: [spring, parameter]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

## HttpServletRequest
- **View** 에서 **Controller**로 parameter전달시 get과 post방식을 가리지 않고 모두 받는다.

```java
@GetMapping("/test1")
public String test1(HttpServletRequest request) {
    String data1 = request.getParameter("data1");
    String data2 = request.getParameter("data2");
    String[] data3 = request.getParameterValues("data3");
    
    return "result";
}
```

## WebRequest
- HttpServletRequest 클래스를 확장한 Class
- 사용방법은 HttpServletRequest과 동일하다.
- 약간의 기능이 추가되어있다고 생각하면 된다.

```java
@GetMapping("/test3")
public String test3(WebRequest request) {
    String data1 = request.getParameter("data1");
    String data2 = request.getParameter("data2");
    String[] data3 = request.getParameterValues("data3");
    
    return "result";
}
```

## @PathVariable
- 데이터가 요청 주소에 있을 때 값을 주입받을 수 있는 어노테이션
- Restful API 서버 프로그래밍시 많이 사용하는 방법

```java
@GetMapping("/test4/{data1}/{data2}/{data3}")
public String test4(@PathVariable String data1,
                    @PathVariable String data2,
                    @PathVariable String data3) {
    
    return "result";
}
```

## @RequestParam


```java
@GetMapping("/test5")
public String test5(@RequestParam int data1,
                    @RequestParam int data2,
                    @RequestParam int [] data3) {
    return "result";
}
// value : 파라미터 이름과 변수의 이름이 다를 때 사용
@GetMapping("/test6")
public String test6(@RequestParam(value = "data1") int value1,
                    @RequestParam(value = "data2") int value2,
                    @RequestParam(value = "data3") int [] value3) {
    return "result";
}
// required : null 허용, defaultValue = null값일시 기본값 설정
@GetMapping("/test7")
public String test7(@RequestParam int data1,
                    @RequestParam (required = false) String data2,
                    @RequestParam (defaultValue = "0") int data3) {
    
    return "result";
}
```


## 참고 .jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<a href="test1?data1=100&data2=200&data3=300&data3=400">test1 get</a><br/>
	<hr/>
	<form action="test2" method="post">
		data 1 : <input type="text" name="data1"/><br/>
		data 2 : <input type="text" name="data2"/><br/>
		data 3 : <input type="checkbox" name="data3" value="100"/>data3 100
				 <input type="checkbox" name="data3" value="200"/>data3 200<br/>
		<button type="submit">test2 post</button>
	</form>
	
	<a href="test3?data1=100&data2=200&data3=300&data3=400">test3 get</a><br/>
	
	<a href="test4/100/200/300">test4</a><br/>

    <hr/>
	<a href='test5?data1=100&data2=200&data3=300&data3=400'>test5</a><br/>
	
	<hr/>
	<a href='test6?data1=100&data2=200&data3=300&data3=400'>test6</a><br/>
	
	<hr/>
	<a href='test7?data1=100'>test7</a><br/>
</body>
</html>
```

> 출처 :  [인프런 - 윤재성의 만들면서 배우는 Spring MVC 5](https://www.inflearn.com/course/spring-mvc5-project)
