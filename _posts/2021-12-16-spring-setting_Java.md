---
layout: single
title: "Spring setting - Java"
categories: spring
tag: [spring, setting, java]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

# spring - xml 셋팅과의 비교
- web.xml = `AbstractAnnotationConfigDispatcherServletInitializer` 상속  
            혹은 `WebApplicationInitializer` 인터페이스 구현

- root-context.xml = 상속없음
- servlet-context.xml = `WebMvcConfigurer` 인터페이스 구현

# spring - ServletAppContext
- `WebApplicationInitializer` 인터페이스 구현

```java
public class SpringConfigClass implements WebApplicationInitializer{

	@Override
	public void onStartup(ServletContext servletContext) throws ServletException {
		// Spring MVC 프로젝트 설정을 위해 작성하는 클래스의 객체를 생성한다.
		AnnotationConfigWebApplicationContext servletAppContext = new AnnotationConfigWebApplicationContext();
		servletAppContext.register(ServletAppContext.class);
		
		// 요청 발생시 요청을 처리하는 서블릿을 DispacherServlet으로 설정한다.
		DispatcherServlet dispatcherServlet = new DispatcherServlet(servletAppContext);
		ServletRegistration.Dynamic servlet = servletContext.addServlet("dispatcher", dispatcherServlet);
		
		// 부가 설정
		servlet.setLoadOnStartup(1);
		servlet.addMapping("/");
		
		// Bean을 정의하는 클래스를 지정한다.
		AnnotationConfigWebApplicationContext rootAppContext = new AnnotationConfigWebApplicationContext();
		rootAppContext.register(RootAppContext.class);
		
		ContextLoaderListener listener = new ContextLoaderListener(rootAppContext);
		servletContext.addListener(listener);
		
		// 파라미터 인코딩 설정
		FilterRegistration.Dynamic filter = servletContext.addFilter("encodingFilter", CharacterEncodingFilter.class);
		filter.setInitParameter("encoding", "UTF-8");
		filter.addMappingForServletNames(null, false, "dispatcher");
	}

}
```

- `AbstractAnnotationConfigDispatcherServletInitializer` 상속  

```java
public class SpringConfigClass extends AbstractAnnotationConfigDispatcherServletInitializer{
	
	// DispatcherServlet에 매핑할 요청 주소를 찾는다
	@Override
	protected String[] getServletMappings() {
		return new String[] {"/"};
	}
	
	// Spring MVC 프로젝트 설정을 위한 설정을 지정한다.
	@Override
	protected Class<?>[] getServletConfigClasses() {
		return new Class[] {ServletAppContext.class};
	}
	
	// 프로젝트에서 사용할 빈들을 정의하기 위한 클래스를 지정한다.
	@Override
	protected Class<?>[] getRootConfigClasses() {
		return new Class[] {RootAppContext.class};
	}

	// 파라미터 인코딩 필터 설정
	@Override
	protected Filter[] getServletFilters() {
		CharacterEncodingFilter encodingFilter = new CharacterEncodingFilter();
		encodingFilter.setEncoding("UTF-8");
		return new Filter[] {encodingFilter};
	}
}
```

# spring - RootAppContext
- Bean을 정의할 Class

```java
// 프로젝트 작업시 사용할 bean을 정희하는 클래스
@Configuration
public class RootAppContext {
    // 필요한 Bean을 설정하면 된다.
}
```

# spring - ServletAppContext

```java
// Spring MVC 프로젝트에 관련된 설정을 하는 클래스
@Configuration
// Controller 어노테이션이 셋팅되어있는 클래스를 Controller로 등록한다.
@EnableWebMvc
// 스캔할 패키지를 지정한다.
@ComponentScan("kr.co.softcampus.controller")
public class ServletAppContext implements WebMvcConfigurer{
	
	// Controller의 메서드가 반환하는 jsp의 이름 앞뒤의 경로와 확장자를 붙혀주도록 설정한다.
	@Override
	public void configureViewResolvers(ViewResolverRegistry registry) {
		WebMvcConfigurer.super.configureViewResolvers(registry);
		registry.jsp("/WEB-INF/views/", ".jsp");
	}
	
	// 정적파일의 경로를 매핑한다.
	@Override
	public void addResourceHandlers(ResourceHandlerRegistry registry) {
		WebMvcConfigurer.super.addResourceHandlers(registry);
		registry.addResourceHandler("/**").addResourceLocations("/resources/");
	}
}
```

### 출처 [인프런 - 윤재성의 만들면서 배우는 Spring MVC 5]