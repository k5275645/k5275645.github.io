---
layout: single
title: "Java - Inner Class"
categories: java
tag: [java, innerClass]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---

> ## 내부 클래스란? (inner class)
- 클래스 내부에 선언한 클래스로 이 클래스를 감싸고 있는 외부 클래스와 밀접한 연관이 있는 경우가 많고, 다른 외부 클래스에서 사용할 일이 거의 없는 경우에 내부 클래스로 선언해서 사용함
- 중첩 클래스라고도 함
- 내부 클래스의 종류
    - 인스턴스 내부 클래스
    - 정적(static) 내부 클래스
    - 지역(local) 내부 클래스
    - 익명(anonymous) 내부 클래스

> ## 인스턴스 내부 클래스
- 내부적으로 사용할 클래스를 선언 (private으로 선언하는 것을 권장)
- 외부 클래스가 생성된 후 생성됨 ( 정적 내부 클래스와 다름 )
- private이 아닌 내부 클래스는 다른 외부 클래스에서 생성할 수 있음

```java
class OutClass {

	private int outNum = 10;
	private static int outStaticNum = 20;
	private InClass inClass;
	
	public OutClass() {
		inClass = new InClass();
	}
	
	private class InClass{
		
		int inNum = 100;
		static int inStaticNum = 200;
		
		void inTest(){
			System.out.println("OutClass outNum = " + outNum + "(외부 클래스의 인스턴스 변수)");
			System.out.println("OutClass outStaticNum = " + outStaticNum + "(외부 클래스의 스태틱 변수)");
			System.out.println("InClass inNum = " + inNum + "(내부 클래스의 인스턴스 변수)");
			System.out.println("InClass inStaticNum = " + inStaticNum + "(내부 클래스의 스태틱 변수)"); // 외부클래스가 생성될 때 생성되기 때문에 원래 안되야함?
		}
	}
	
	public void usingClass() {
		inClass.inTest();
	}
}

public class InnerTest {
	public static void main(String[] args) {
		OutClass outClass = new OutClass();
		outClass.usingClass();
	}
}
```

> ## 정적 내부 클래스
- 외부 클래스 생성과 무관하게 사용할 수 있음
- 정적 변수, 정적 메서드 사용

```java
class OutClass {

	private int outNum = 10;
	private static int outStaticNum = 20;
	
	static class InStaticClass {
		
		int inNum = 100;
		static int inStaticNum = 200;
		
		void inTest(){
			//System.out.println("OutClass num = " + outNum + "(외부 클래스의 인스턴스 변수)"); -> 사용불가
			System.out.println("OutClass sNum = " + outStaticNum + "(외부 클래스의 스태틱 변수)");
			System.out.println("InClass inNum = " + inNum + "(내부 클래스의 인스턴스 변수)");
			System.out.println("InClass inNum = " + inStaticNum + "(내부 클래스의 스태틱 변수)");
		}
		
		static void inStaticTest(){
			//System.out.println("OutClass num = " + outNum + "(외부 클래스의 인스턴스 변수)"); -> 사용불가
			System.out.println("OutClass sNum = " + outStaticNum + "(외부 클래스의 스태틱 변수)");
			//System.out.println("InClass inNum = " + inNum + "(내부 클래스의 인스턴스 변수)"); -> 사용불가
			System.out.println("InClass inNum = " + inStaticNum + "(내부 클래스의 스태틱 변수)");
		}
	}
}

public class InnerTest {
	public static void main(String[] args) {
		OutClass.InStaticClass inStaticClass = new OutClass.InStaticClass();
		inStaticClass.inTest();
		System.out.println("-------------------");
		OutClass.InStaticClass.inStaticTest();
	}
}
```

> ## 지역(local) 내부 클래스
- 지역 변수와 같이 메서드 내부에서 정의하여 사용하는 클래스
- 메서드의 호출이 끝나면 메서드에 사용된 지역변수의 유효성은 사라짐
- 메서드 호출 이후에도 사용해야 하는 경우가 있을 수 있으므로 지역 내부 클래스에서 사용하는 메서드의 지역 변수나 매개 변수는 final로 선언됨

```java

```

> ## 익명(anonymous) 내부 클래스

> 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.](https://fastcampus.co.kr/dev_online_javaend)