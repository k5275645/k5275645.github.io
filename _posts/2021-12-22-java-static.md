---
layout: single
title: "Java - static, singleton"
categories: java
tag: [static, singleton]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---

## static
- 인스턴스 생성과 상관없이 할당
- 인스턴스에서 공동으로 사용하는 영역
- static 변수와 메서드는 인스턴스 변수와 메서드가 아니므로 클래스 이름으로 직접참조
- 여러 인스턴스에서 공통으로 사용할 변수와 메서드는 static으로 구현할 수 있다.

## singleton pattern
- 인스턴스가 단 한개만 생성되어야 하는 경우 사용
- static 변수, 메서드를 활용해서 구현

```java
public class Company {

    private static Company instance = new Company();

    private Company() {}

    public static Company getInstance () {

        if (instance == null) {
            instance = new Company();
        }

        return instance;
    }
}
```

- test

```java
public class Test {
    public static void main(String[] args) {

        Company c1 = Company.getInstance();
        Company c2 = Company.getInstance();
        System.out.println(c1); // test.Company@379619aa
		System.out.println(c2); // test.Company@379619aa
    }
}
```

## Practice
- 자동차 공장이 있다.  
자동차 공장은 유일한 객체.  
공장에서 자동차는 제작될 때마다 고유의 번호가 부여.  
자동차 번호는 10001 부터 부여.  
자동차 공장 클래스, 자동차 클래스를 구현하라.  
CarFactoryTest.java 테스트 코드가 수행 되도록 하라.

- CarFactoryTest.java

```java
public class CarFactoryTest {
	public static void main(String[] args) {
		CarFactory factory = CarFactory.getInstance();
		Car mySonata = factory.createCar();
		Car yourSonata = factory.createCar();
		
		System.out.println(mySonata.getCarNum());   // 10001
		System.out.println(yourSonata.getCarNum()); // 10002
	}
}
```

- CarFactory.java

```java
public class CarFactory {

	private static CarFactory instance = new CarFactory();
	
	private CarFactory() {}
	
	public static CarFactory getInstance() {
		if(instance == null) {
			instance = new CarFactory();
		}
		return instance;
	}
	
	public Car createCar() {
		
		Car car = new Car();
		return car;
	}
}
```

- Car.java

```java
public class Car {

	private static int serialNum = 10000;
	private int carNum;
	
	public Car() {
		serialNum++;
		carNum = serialNum;
	}

	public int getCarNum() {
		return carNum;
	}

	public void setCarNum(int carNum) {
		this.carNum = carNum;
	}
}
```

> 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.](https://fastcampus.co.kr/dev_online_javaend)

