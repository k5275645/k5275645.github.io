---
layout: single
title: "Spring - ViewResolver"
categories: spring
tag: [spring, ViewResolver]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

- # @Controller

```java
@Controller
public class TestController {
	
	@GetMapping("/test1")
	public String test1() {
		return "test1";
	}
	
	@GetMapping("/test2")
	public String test2(HttpServletRequest request) {
		
		request.setAttribute("data1", 100);
		request.setAttribute("data2", 200);
		
		return "test2";
	}
	
	@GetMapping("/test3")
	public String test3(Model model) {
		model.addAttribute("data1", 300);
		model.addAttribute("data2", 400);
		return "test3";
	}
	
	@GetMapping("/test4")
	public ModelAndView test4(ModelAndView mv) {
		mv.addObject("data1", 500);
		mv.addObject("data2", 600);
		mv.setViewName("test4");
		return mv;
	}
}
```

- # View(.jsp)

## index.jsp
```jsp
<body>
    <!-- parameter도 ModelAndView에 담겨서 jsp에 전달된다. -->
	<a href="test1?data1=100&data2=200">test1</a>
	<hr/>
	<a href="test2">test2</a>
	<hr/>
	<a href="test3">test3</a>
	<hr/>
	<a href="test4">test4</a>
</body>
```

## test1.jsp
```jsp
<body>
	<h1>test1</h1>
	<h3>data1 : ${param.data1}</h3> <!-- 100 -->
	<h3>data2 : ${param.data2}</h3> <!-- 200 -->
</body>
```

## test2.jsp
```jsp
<body>
	<h1>test2</h1>
	<h3>data1 : ${requestScope.data1}</h3> <!-- 100 -->
	<h3>data2 : ${requestScope.data2}</h3> <!-- 200 -->
</body>
```

## test3.jsp
```jsp
<body>
	<h1>test3</h1>
	<h3>data1 : ${requestScope.data1}</h3> <!-- 300 -->
	<h3>data2 : ${requestScope.data2}</h3> <!-- 400 -->
</body>
```

## test4.jsp
```jsp
<body>
	<h1>test4</h1>
	<h3>data1 : ${requestScope.data1}</h3> <!-- 500 -->
	<h3>data2 : ${requestScope.data2}</h3> <!-- 600 -->
</body>
```


###### 출처 [인프런 - 윤재성의 만들면서 배우는 Spring MVC 5]
