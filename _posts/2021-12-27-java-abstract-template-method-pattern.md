---
layout: single
title: "java - abstract-template method pattern"
categories: java
tag: [abstract, template method pattern]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---

<div class="notice--success">
<h4>템플릿 메서드</h4>
<ul>
    <li>추상 메서드나 구현 된 메서드를 활용하여 코드의 흐름(시나리오)를 정의하는 메서드</li>
    <li>final로 선언하여 하위 클래스에서 재정의 할 수 없게 함</li>
    <li>프레임워크에서 많이 사용되는 설계 패턴</li>
    <li>추상 클래스로 선언된 상위 클래스에서 템플릿 메서드를 활용하여 전체적인 흐름을 정의 하고 하위 클래스에서 다르게 구현되어야 하는 부분은 추상 메서드로 선언하여 하위 클래스에서 구현 하도록 함</li>
</ul>
</div>

## Car 클래스(추상)
```java
public abstract class Car {
	
	public abstract void drive();
	public abstract void stop();
	
	public void startCar() {
		System.out.println("시동을 켭니다.");
	}
	
	public void turnOff() {
		System.out.println("시동을 끕니다.");
	}

    // 코드의 흐름(시나리오)를 여기서 정의
    // 하위클래스에서 재정의를 막기위해 final로 선언
	final public void run() {
		startCar();
		drive();
		stop();
		turnOff();
	}
}
```

## AICar 클래스(Car 클래스 상속)
```java
public class AICar extends Car{
    @Override
    public void drive() {
        System.out.println("자율 주행합니다.");
        System.out.println("자동차가 스스로 방향을 바꿉니다.");
    }

    @Override
    public void stop() {
        System.out.println("스스로 멈춥니다.");		
    }
}
```

## ManualCar 클래스(Car 클래스 상속)
```java
public class ManualCar extends Car{
	@Override
	public void drive() {
		System.out.println("사람이 운전합니다.");
		System.out.println("사람이 핸들을 조작합니다.");		
	}

	@Override
	public void stop() {
		System.out.println("브레이크를 밟아서 정지합니다.");		
	}
}
```

## CarTest 클래스
```java
public class CarTest {

	public static void main(String[] args) {
		
		Car aiCar = new AICar();
		aiCar.run();
        /*
        시동을 켭니다.
        자율 주행합니다.
        자동차가 스스로 방향을 바꿉니다.
        스스로 멈춥니다.
        시동을 끕니다.
        */
		
		Car manualCar = new ManualCar();
		manualCar.run();
        /*
        시동을 켭니다.
        사람이 운전합니다.
        사람이 핸들을 조작합니다.
        브레이크를 밟아서 정지합니다.
        시동을 끕니다.
        */
	}
}
```

###### 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.]