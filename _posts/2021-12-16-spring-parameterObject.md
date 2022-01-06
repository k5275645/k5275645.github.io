---
layout: single
title: "Spring - getParameterObject"
categories: spring
tag: [spring, parameter]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

## @RequestParam - Object


```java
@GetMapping("/test1")
public String test1(@RequestParam Map<String, String> map, @RequestParam List<String> data3) {
    String data1 = map.get("data1");
    String data2 = map.get("data2");
    for (String str : data3) {
        //
    }
    return "result";
}

@GetMapping("test2")
// @ModelAttribute 는 생략이 가능하다.
// @ModelAttribute를 사용하면 전달되는 이름과 동일한 프로퍼티에 자동으로 주입된다.
// 이러한 객체를 커맨드 객체(Command Object)라고 한다.
//public String test2(@ModelAttribute DataBean bean1, @ModelAttribute DataBean2 bean2) {
public String test2(DataBean bean1, DataBean2 bean2) {
    
    for(int number1 : bean1.getData3()) {
        //
    }
    
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
	<a href="test1?data1=100&data2=200&data3=300&data3=400">test1 get</a>
	<hr/>
	<a href="test2?data1=100&data2=200&data3=300&data3=400">test2 get</a>
</body>
</html>
```

## 참고 Bean

```java
public class DataBean {

	private int data1;
	private int data2;
	private int[] data3;
	
	public int getData1() {
		return data1;
	}
	public void setData1(int data1) {
		this.data1 = data1;
	}
	public int getData2() {
		return data2;
	}
	public void setData2(int data2) {
		this.data2 = data2;
	}
	public int[] getData3() {
		return data3;
	}
	public void setData3(int[] data3) {
		this.data3 = data3;
	}
}
```

```java
public class DataBean2 {
	
	private int data1;
	private int data2;
	
	public int getData1() {
		return data1;
	}
	public void setData1(int data1) {
		this.data1 = data1;
	}
	public int getData2() {
		return data2;
	}
	public void setData2(int data2) {
		this.data2 = data2;
	}
}
```

> 출처 :  [인프런 - 윤재성의 만들면서 배우는 Spring MVC 5](https://www.inflearn.com/course/spring-mvc5-project)


