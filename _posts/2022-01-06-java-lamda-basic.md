---
layout: single
title: "Java - lamda"
categories: java
tag: [java, lamda, FunctionalInterface]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

> ## 람다

- 자바는 객체 지향 프로그래밍 : 기능을 수행하긴 위해서는 객체를 만들고 그 객체 내부에 멤버 변수를 선언하고 기능을 수행하는 메서드를 구현
- 자바 8부터 함수형 프로그래밍 방식을 지원하고 이를 람다식이라 함
- 함수의 구현과 호출만으로 프로그래밍이 수행되는 방식
- 함수형 프로그래밍(Functional Programming: FP)
    - 함수형 프로그래밍은 순수함수(pure function)를 구현하고 호출함으로써 외부 자료에 부수적인 영향(side effect)를 주지 않도록 구현하는 방식입니다. 
    - 순수 함수란 매개변수만을 사용하여 만드는 함수 입니다. 즉, 함수 내부에서 함수 외부에 있는 변수를 사용하지 않아 함수가 수행되더라도 외부에는 영향을 주지 않습니다.
    - 함수를 기반으로 하는 프로그래밍이고 입력받는 자료 이외에 외부 자료를 사용하지 않아 여려 자료가 동시에 수행되는 병렬처리가 가능합니다.
    - 함수형 프로그래밍은 함수의 기능이 자료에 독립적임을 보장합니다. 이는 동일한 자료에 대해 동일한 결과를 보장하고, 다양한 자료에 대해 같은 기능을 수행할 수 있습니다.


>> ## 예시

```java
// 인터페이스
public interface Add {
	public int add(int x, int y);
}
```

```java
public static void main(String[] args) {
		
    // 람다식 X
    Add add = new Add() {
        @Override
        public int add(int x, int y) {
            return x+y;
        }
    };
    
    // 람다식
    Add add2 = (x, y) -> {
        return x+y;
    };
    
    // 람다식 축약
    Add add3 = (x, y) -> x + y;
    
    System.out.println(add.add(10, 20)); // 30
    System.out.println(add2.add(30, 40)); // 70
    System.out.println(add3.add(50, 60)); // 110

}
```

>> ## 함수형 인터페이스 선언하기 (@FunctionalInterface)
- 람다식을 선언하기 위한 인터페이스
- 익명 함수와 매개 변수만으로 구현되므로 인터페이스는 단 하나의 메서드만을 선언해야함
- @FunctionalInterface 애노테이션(annotation)
함수형 인터페이스라는 의미, 내부에 여러 개의 메서드를 선언하면 에러남

```java
@FunctionalInterface
public interface MyNumber {
	int getMax(int num1, int num2);
    //int getMin(int num1, int num2); -> 에러
}
```

```java
public static void main(String[] args) {
    MyNumber max = (x, y)->(x >= y) ? x : y; // 람다식을 인터페이스 자료형 max 변수에 대입

    System.out.println(max.getMax(10, 20));// 인터페이스 자료형 변수로 함수 호출
}
```