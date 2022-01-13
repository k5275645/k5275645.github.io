---
layout: single
title: "Java - stream"
categories: java
tag: [java, stream]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

> ## 스트림이란?

- **자료의 대상과 관계없이 동일한 연산을 수행**  
배열, 컬렉션을 대상으로 연산을 수행 함  
일관성 있는 연산으로 자료의 처리를 쉽고 간단하게 함  
자료 처리에 대한 추상화가 구현되었다고 함  


- **한번 생성하고 사용한 스트림은 재사용 할 수 없음**  
자료에 대한 스트림을 생성하여 연산을 수행하면 스트림은 소모됨  
다른 연산을 수행하기 위해서는 스트림을 다시 생성해야 함  


- **스트림 연산은 기존 자료를 변경하지 않음**  
자료에 대한 스트림을 생성하면 스트림이 사용하는 메모리 공간은 별도로 생성되므로 연산이 수행되도 기존 자료에 대한 변경은 발생하지 않음  


- **스트림 연산은 중간 연산과 최종 연산으로 구분 됨**  
스트림에 대해 중간 연산은 여러 개의 연산이 적용될 수 있지만 최종 연산은 마지막에 한 번만 적용됨  
최종연산이 호출되어야 중간 연산에 대한 수행이 이루어 지고 그 결과가 만들어짐  
따라서 중간 연산에 대한 결과를 연산 중에 알수 없음  
이를 '지연 연산'이라 함  

>> ### 기본 예시

```java
public static void main(String[] args) {
  int[] testArr = {1,2,3,4,5};
  
  // 스트림 사용X
  for(int num : testArr) {
    System.out.print(num); // 12345
  }

  // 스트림
  Arrays.stream(testArr).forEach(e -> System.out.print(e)); // 12345
}
```


> ## 중간 연산과 최종 연산

- 중간 연산의 예 - filter(), map(), sorted() 등 조건에 맞는 요소를 추출(filter)하거나 요소를 변환 함(map)
- 최종 연산의 예 - forEach(), count(), sum() 등  
스트림이 관리하는 자료를 하나씩 소모해가며 연산이 수행 됨  
최종 연산 후에 스트림은 더 이상 다른 연산을 적용할 수 없음  
- 최종 연산이 호출될 때 중간 연산이 수행되고 결과가 생성 됨
- 중간 연산과 최종 연산에 대한 구현은 람다식을 활용함

>> ### 중간 연산과 최종 연산 예시

```java
List<String> sList = new ArrayList<String>();
sList.add("ccc");
sList.add("bb");
sList.add("a");

Stream<String> sStream = sList.stream();
sStream.forEach(s->System.out.print(s)); // cccbba
sList.stream().sorted().forEach(s->System.out.print(s)); // abbccc
sList.stream().map(s->s.length()).forEach(s->System.out.print(s)); // 321
sList.stream().filter(s -> s.length() >= 2).forEach(s->System.out.print(s)); // cccbb 
```

> ## 객체지향 프로그래밍과 람다식 비교

- StringConcat interface

```java
@FunctionalInterface
public interface StringConcat {
	public void makeString(String str1, String str2);
}
```

- StringConcatImpl Class

```java
public class StringConcatImpl implements StringConcat{
	@Override
	public void makeString(String str1, String str2) {
		System.out.println(str1 + ", " + str2);	
	}
}
```

- Test Class

```java
public class StringConcatTest {

	public static void main(String[] args) {
		
		String str1 = "str1";
		String str2 = "str2";
		
		// 객체지향으로 구현
		StringConcatImpl stringConcatImpl = new StringConcatImpl();
		stringConcatImpl.makeString(str1, str2); // str1, str2
		
		// 람다식으로 구현
		StringConcat stringConcat = (s1, s2) -> System.out.println(s1 + " : " + s2);
		stringConcat.makeString(str1, str2); // str1 : str2
		
		// 익명 객체를 사용하는 람다식
		StringConcat stringConcat2 = new StringConcat() {

			@Override
			public void makeString(String str1, String str2) {
				System.out.println(str1 + "..." + str2);
			}

		};
		stringConcat2.makeString(str1, str2); // str1...str2
	}
}
```

> ## reduce() 연산

- Stream 최종연산자
- Stream 요소를 하나씩 줄여가며 누적연산 수행

```java
class CompareString implements BinaryOperator<String>{
	@Override
	public String apply(String s1, String s2) {
		if (s1.getBytes().length >= s2.getBytes().length) {
			return s1;
		} else {
			return s2;
		}
	}
	
}

public class Test {
	public static void main(String[] args) {
		
		String[] strArr = {"a", "bb", "ccc"};
		
		String resultStr1 = Arrays.stream(strArr).reduce("", (s1, s2) -> {
			if (s1.getBytes().length >= s2.getBytes().length) {
				return s1;
			} else {
				return s2;
			}
		});
		System.out.println(resultStr1); // ccc
		
		String resultStr2 = Arrays.stream(strArr).reduce(new CompareString()).get(); // BinaryOperator를 구현한 클래스 이용 
		System.out.println(resultStr2); // ccc
	}
}
```


>> ### 활용 예제

```
여행사에 패키지 여행 상품이 있습니다. 여행 비용은 15세 이상은 100만원, 그 미만은 50만원 입니다. 
고객 세 명이 패키지 여행을 떠난다고 했을 때 비용 계산과 고객 명단 검색등에 대한 연산을 스트림을 활용하여 구현해 봅니다.
고객에 대한 클래스를 만들고 ArrayList로 고객을 관리 합니다. 

고객 정보는 다음과 같습니다.

CustomerLee 
이름 : 이순신
나이 : 40
비용 : 100

CustomerKim
이름 : 김유신
나이 : 20 
비용 : 100

CustomerHong
이름 : 홍길동
나이 :13
비용 : 50
```


>> ## TravelCustomer 클래스

```java
public class TravelCustomer {

	private String name;   //이름
	private int age;       //나이
	private int price;     //가격
	
	public TravelCustomer(String name, int age, int price) {
		this.name = name;
		this.age = age;
		this.price = price;
	}

	public String getName() {
		return name;
	}

	public int getAge() {
		return age;
	}

	public int getPrice() {
		return price;
	}
	
	public void setName(String name) {
		this.name = name;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public void setPrice(int price) {
		this.price = price;
	}

	public String toString() {
		return "name: " + name + "age: " + age + "price: " + price; 
	}

}
```

>> ### Test 클래스

```java
public class TravelTest {

	public static void main(String[] args) {
		TravelCustomer customerLee = new TravelCustomer("이순신", 40, 100);
		TravelCustomer customerKim = new TravelCustomer("김유신", 20, 100);
		TravelCustomer customerHong = new TravelCustomer("홍길동", 13, 50);
		
		List<TravelCustomer> customerList = new ArrayList<>();
		customerList.add(customerLee);
		customerList.add(customerKim);
		customerList.add(customerHong);
		
		System.out.println("== 고객 명단 추가된 순서대로 출력 ==");
		customerList.stream().map(c->c.getName()).forEach(s->System.out.println(s)); // 이순신 김유신 홍길동
		
		int total = customerList.stream().mapToInt(c->c.getPrice()).sum();
		System.out.println("총 여행 비용은 :" + total + "입니다"); // 총 여행 비용은 :250입니다
		
		System.out.println("== 20세 이상 고객 명단 정렬하여 출력 ==");
		customerList.stream().filter(c->c.getAge() >= 20).map(c->c.getName()).sorted().forEach(s->System.out.println(s)); // 김유신 이순신
	}

}
```

> 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.](https://fastcampus.co.kr/dev_online_javaend)