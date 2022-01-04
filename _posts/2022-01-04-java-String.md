---
layout: single
title: "String"
categories: java
tag: [java, String]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---

> ## String
>> ### String 선언방법

```java
// 힙 메모리에 인스턴스로 생성되는 경우
// 힙 메모리는 생성될때마다 다른 주소 값을 가짐
String str1 = new String("abc");
String str2 = new String("abc");

System.out.println(str1 == str2); // false

// 상수 풀(constant pool)에 있는 주소를 참조하는 경우
// 상수 풀의 문자열은 모두 같은 주소 값을 가짐
String str3 = "abc";
String str4 = "abc";

System.out.println(str3 == str4); // true
```

>> ### String을 연결하면 기존의 String에 연결되는 것이 아닌 새로운 문자열이 생성됨 ( 메모리 낭비가 발생할 수도 )

```java
String abc = new String("abc");
String def = new String("def");

System.out.println(System.identityHashCode(abc)); // 474675244

abc = abc.concat(def);

System.out.println(System.identityHashCode(abc)); // 305808283
```

>> ### StringBuilder, StringBuffer 활용하기
- 내부적으로 가변적인 char[]를 멤버 변수로 가짐
- 문자열을 여러번 연결하거나 변경할 때 사용하면 유용함
- 새로운 인스턴스를 생성하지 않고 char[] 를 변경함
- StringBuffer는 멀티 쓰레드 프로그래밍에서 동기화(synchronization)을 보장
- 단일 쓰레드 프로그램에서는 StringBuilder 사용을 권장
- toString() 메서드로 String반환

```java
String abc = new String("abc");
String def = new String("def");

StringBuilder builder = new StringBuilder(abc);

System.out.println(System.identityHashCode(builder)); // 474675244

builder.append(def);

System.out.println(System.identityHashCode(builder)); // 474675244

System.out.println(builder.toString()); // abcdef
```

