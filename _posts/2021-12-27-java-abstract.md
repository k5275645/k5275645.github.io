---
layout: single
title: "Java - abstract"
categories: java
tag: [abstract]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
published: false
---

## 추상 클래스(상위 클래스)

```java
public abstract class  Computer {

	abstract void display(); // 구현부는 상속받은 클래스에서
	abstract void typing(); // 구현부는 상속받은 클래스에서
	
	public void turnOn() {
		System.out.println("전원을 켭니다.");
	}
	
	public void turnOff() {
		System.out.println("전원을 끕니다.");
	}
}
```

## 하위 클래스

```java
public class DeskTop extends Computer{

    // 추상 메서드 구현
	@Override
	void display() {
		System.out.println("DeskTop display");
	}

    // 추상 메서드 구현
	@Override
	void typing() {
		System.out.println("DeskTop typing");
	}

    // 상위 클래스의 메서드 재정의 가능
	@Override
	public void turnOff() {
		System.out.println("Desktop turnoff");
	}
}
```

## 하위 클래스 일부 메서드 구현(추상 클래스로 선언시)

```java
public abstract class NoteBook extends Computer{
	@Override
	public void typing() {
		System.out.println("NoteBook typing");		
	}
}
```

## 추상클래스를 상속받은 추상클래스를 다시 상속
```java
public class MyNoteBook extends NoteBook{
	@Override
	void display() {
		System.out.println("MyNoteBook display");		
	}
}
```

## Test
```java
public class ComputerTest {

	public static void main(String[] args) {
        /*
        추상 클래스 Computer, NoteBook은 new ---(); 로 구현될 수 없다.
        이를 구현한 클래스인 DeskTop, MyNoteBook 으로 구현된다.

        상속에서 upcasting은 묵시적으로 가능하다.
        이 경우 Computer에서 정의된 메서드만 사용가능하다.
        만약, DeskTop에 새롭게 정의한 메서드가 있으면 
        아래와 같은 선언에서는 사용할 수 없다.
        */

		Computer computer = new DeskTop();
		computer.display(); // DeskTop display
		computer.turnOff(); // Desktop turnoff
		computer.turnOn();  // 전원을 켭니다.
		computer.typing();  // DeskTop typing

		NoteBook myNote = new MyNoteBook();
		myNote.display(); // MyNoteBook display
		myNote.turnOff(); // 전원을 끕니다.
		myNote.turnOn();  // 전원을 켭니다.
		myNote.typing();  // NoteBook typing

		MyNoteBook myNoteBook = new MyNoteBook();
		myNoteBook.display(); // MyNoteBook display
		myNoteBook.turnOff(); // 전원을 끕니다.
		myNoteBook.turnOn();  // 전원을 켭니다.
		myNoteBook.typing();  // NoteBook typing
	}
}
```

> 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.](https://fastcampus.co.kr/dev_online_javaend)


