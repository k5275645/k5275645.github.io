---
layout: single
title: "Generic"
categories: java
tag: [java, Generic]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---

> ## 제네릭 자료형 정의
- 클래스에서 사용하는 변수의 자료형이 여러개 일수 있고, 그 기능(메서드)은 동일한 경우 클래스의 자료형을 특정하지 않고 추후 해당 클래스를 사용할 때 지정 할 수 있도록 선언
- 실제 사용되는 자료형의 변환은 컴파일러에 의해 검증되므로 안정적인 프로그래밍 방식
- 컬렉션 프레임워크에서 많이 사용되고 있음

> ## 참고 클래스


```java
public class Powder {
	public String toString() {
		return "재료는 Powder 입니다";
	}
}
```

```java
public class Plastic {
	public String toString() {
		return "재료는 Plastic 입니다";
	}
}
```

> ## 제네릭 타입을 사용하지 않는 경우의 예

- 재료가 Powder인 경우


```java
public class ThreeDPrinter1{
	private Powder material;
	
	public void setMaterial(Powder material) {
		this.material = material;
	}
	
	public Powder getMaterial() {
		return material;
	}
}
```


- 재료가 Plastic인 경우


```java
public class ThreeDPrinter2{
	private Plastic material;
	
	public void setMaterial(Plastic material) {
		this.material = material;
	}
	
	public Plastic getMaterial() {
		return material;
	}
}
```

- 여러 타입을 대체하기 위해 Object를 사용할 수 있음


```java
public class ThreeDPrinter{

	private Object material;
	
	public void setMaterial(Object material) {
		this.material = material;
	}
	
	public Object getMaterial() {
		return material;
	}
}
```

- test


```java
ThreeDPrinter printer = new ThreeDPrinter();

Powder powder = new Powder();
printer.setMaterial(powder);

// Powder p = printer.getMaterial(); -> 타입오류발생
Powder p = (Powder)printer.getMaterial();
```


> ## 제네릭 타입을 사용한 경우의 예

```java
public class GenericPrinter<T> {

	private T material;
	
	public void setMaterial(T material) {
		this.material = material;
	}
	
	public T getMaterial() {
		return material;
	}
	
	public String toString(){
		return material.toString();
	}
}
```

```java
public class GeneriPrinterTest {

	public static void main(String[] args) {

		GenericPrinter<Powder> powderPrinter = new GenericPrinter<Powder>();
		powderPrinter.setMaterial(new Powder());

		System.out.println(powderPrinter); // 재료는 Powder 입니다(.toString() 자동호출)

		GenericPrinter<Plastic> plasticPrinter = new GenericPrinter<Plastic>();

		plasticPrinter.setMaterial(new Plastic());
        
		System.out.println(plasticPrinter.toString()); // 재료는 Plastic 입니다(.toString() 자동호출)
	}
}
```