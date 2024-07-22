---
layout: single
title: "Java - Data Structure"
categories: java
tag: [java, Data Structure]
toc: true
author_profile: false
sidebar: 
    nav: "docs"
published: false
---

> ## 자료구조란 무엇인가? (Data Structure)
- 프로그램에서 사용할 많은 데이타를 메모리 상에서 관리하는 여러 구현방법들
- 효율적인 자료구조가 성능 좋은 알고리즘의 기반이 됨
- 자료의 효율적인 관리는 프로그램의 수행속도와 밀접한 관련이 있음
- 여러 자료 구조 중에서 구현하려는 프로그램에 맞는 최적의 자료구조를 활용해야 하므로 자료구조에 대한 이해가 중요함

> ## 자료구조의 종류
- 선형 자료구조 : 한 줄로 자료를 관리
    - **배열(Array)** : 선형으로 자료를 관리, 정해진 크기의 메모리를 먼저 할당받아 사용하고, 자료의 물리적 위치와 논리적 위치가 같음
    - **연결 리스트 (LinkedList)** : 선형으로 자료를 관리, 자료가 추가될 때마다 메모리를 할당 받고, 자료는 링크로 연결됨. 자료의 물리적 위치와 논리적 위치가 다를 수 있음 리스트에 자료 추가하기
    - **스택 (Stack)** : 가장 나중에 입력 된 자료가 가장 먼저 출력되는 자료 구조 (Last In First OUt)
    - **큐 (Queue)** :  가장 먼저 입력 된 자료가 가장 먼저 출력되는 자료 구조 (First In First Out)
    - **트리 (Tree)** : 부모 노드와 자식 노드간의 연결로 이루어진 자료 구조
    - **그래프 (Graph)** :  정점과 간선들의 유한 집합 G = (V,E)
        - 정점(vertex) : 여러 특성을 가지는 객체, 노드(node)
        - 간선edge() : 이 객체들을 연결 관계를 나타냄. 링크(link)
    - **해싱 (Hashing)** : 자료를 검색하기 위한 자료 구조

> 출처 [패스트 캠퍼스 - 한번에 끝내는 Java/Spring 웹 개발 마스터 초격차 패키지 Online.](https://fastcampus.co.kr/dev_online_javaend)
    