---
layout: single
title: "Java - interface"
categories: java
tag: [interface]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
published: false
---

<div class="notice--success">
<h4>인터페이스가 하는 일</h4>
<ul>
    <li>클래스나 프로그램이 제공하는 기능을 명시적으로 선언</li>
    <li>일종의 클라이언트 코드와의 약속이며 클래스나 프로그램이 제공하는 명세(specification)</li>
    <li>클라이언트 프로그램은 인터페이스에 선언된 메서드 명세만 보고 이를 구현한 클래스를 사용할 수 있음</li>
    <li>어떤 객체가 하나의 인터페이스 타입이라는 것은 그 인터페이스가 제공하는 모든 메서드를 구현했다는 의미임</li>
    <li>인터페이스를 구현한 다양한 객체를 사용함 - 다형성 예) JDBC 인터페이스</li>
</ul>
</div>

<div class="notice--success">
<h4>여러 인터페이스 구현</h4>
<ul>
    <li>자바의 인터페이스는 구현 코드가 없으므로 하나의 클래스가 여러 인터페이스는 구현 할 수 있음</li>
    <li>디폴트 메서드가 중복 되는 경우는 구현 하는 클래스에서 재정의 하여야 함</li>
    <li>여러 인터페이스를 구현한 클래스는 인터페이스 타입으로 형 변환 되는 경우 해당 인터페이스에 선언된 메서드만 사용 가능 함</li>
</ul>
</div>


## Buy 인터페이스
```java
public interface Buy {

	void buy();
	
	default void order() {
		System.out.println("구매 주문");
	}
}
```

## Sell 인터페이스
```java
public interface Sell {

	void sell();
	
	default void order() {
		System.out.println("판매 주문");
	}
}
```

## Customer 클래스(Buy 인터페이스, Sell 인터페이스 구현)
```java
public class Customer implements Buy, Sell{

	@Override
	public void sell() {
		System.out.println("customer sell");
	}

	@Override
	public void buy() {
		System.out.println("customer buy");		
	}

    // 해당 구현에 대한 공통 메서드 이므로 
    // 인터페이스를 특정해 사용을 하던가 재정의를 해서 사용해야함
	@Override
	public void order() {
		System.out.println("customer order"); // 재정의 해서 사용하겠다.
        //Buy.super.order(); -> Buy 인터페이스의 default 메서드를 사용하겠다.
        //Sell.super.order(); -> Sell 인터페이스의 default 메서드를 사용하겠다.
	}

	public void sayHello() {
		System.out.println("Hello");
	}

}
```

## Test 클래스
```java
public class CustomerTest {

	public static void main(String[] args) {

		Customer customer = new Customer();
		customer.buy();         // customer buy
		customer.sell();        // customer sell
		customer.sayHello();    // Hello
		
		Buy buyer = customer;   // up castring
		buyer.buy();            // customer buy
        buyer.order();          // customer order -> 재정의된 메서드가 호출됨
		
		Sell seller = customer; // up castring
		seller.sell();          // customer sell
        seller.order();         // customer order -> 재정의된 메서드가 호출됨
		
		
		
	}
}
```

<div class="notice--success">
<h4>클래스 상속과 인터페이스 구현 함께 쓰기</h4>
<ul>
    <li>실무에서 프레임워크나 오픈소스와 함께 연동되는 구현을 하게 되면 클래스 상속과 인터페이스의 구현을 같이 사용하는 경우가 많음</li>
    <li>책이 순서대로 대여가 되는 도서관 구현</li>
    <li>책을 보관하는 자료 구조가 Shelf에 구현됨 (ArrayList)</li>
    <li>Queue 인터페이스를 구현함</li>
    <li>Shelf 클래스를 상속 받고 Queue를 구현한다.</li>
</ul>
</div>

## Shelf 클래스
```java
public class Shelf {

	 protected ArrayList<String> shelf;
	 
	 public Shelf() {
		 shelf = new ArrayList<String>();
	 }
	 
	 public ArrayList<String> getShelf(){
		 return shelf;
	 }
	 
	 public int getCount() {
		 return shelf.size();
	 }
	 
}
```

## Queue 인터페이스
```java
public interface Queue {

	void enQueue(String title);
	String deQueue();
	int getSize();
}
```

## BookShelf 클래스(Shelf 클래스 상속, Queue 인터페이스 구현)
```java
public class BookShelf extends Shelf implements Queue{

	@Override
	public void enQueue(String title) {
		shelf.add(title); // Shelf 클래스에서 protected로 선언해서 접근할 수 있다.
	}

	@Override
	public String deQueue() {
		return shelf.remove(0);
	}

	@Override
	public int getSize() {
		return getCount();
	}
}
```

## Test 클래스
```java
public class BookShelfTest {

	public static void main(String[] args) {

		Queue bookQueue = new BookShelf();
		bookQueue.enQueue("태백산맥1");
		bookQueue.enQueue("태백산맥2");
		bookQueue.enQueue("태백산맥3");
		
		System.out.println(bookQueue.getSize()); // 3
		System.out.println(bookQueue.deQueue()); // 태백산맥1
		System.out.println(bookQueue.getSize()); // 2
		System.out.println(bookQueue.deQueue()); // 태백산맥2
		System.out.println(bookQueue.getSize()); // 1
		System.out.println(bookQueue.deQueue()); // 태백산맥3
		System.out.println(bookQueue.getSize()); // 0
	}

}
```


> 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.](https://fastcampus.co.kr/dev_online_javaend)