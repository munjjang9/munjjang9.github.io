---
layout: post
title: 프로그래밍 방식
author: munjjang9
tags: [programming method, solid, principle]
date: 2024-11-28 13:30 +0900
categories: [C/C++]
toc: true
---

# 프로그래밍 방식의 발전
---
절차지향(Procedural) → 정보공학(구조체) → 객체지향 → CBD(Component Based Development)

순으로 발전해오고 있다.

<br>

## 객체지향이란?
---
프로그래밍을 하는 방식 중 하나로, 프로그램을 여러 객체들로 구성한다.

객체는 메소드와 변수를 가진다.

<br>

## 객체지향의 특성
---
    1. 정보 은닉

    2. 캡슐화

    3. 상속성

    4. 다형성

    5. 추상성

<br>

### 1. 정보 은닉
---
소프트웨어에서 사용하는 객체에 대한 구체적인 정보를 노출시키지 않도록 하는 기법
- 접근 제한자 사용 : public, private, protected, internal ... 

<br>

### 2. 캡슐화 (블랙박스화)
---
서로 연관있는 속성과 기능들을 하나의 캡슐(capsule)로 만들어 데이터를 외부로부터 보호하는 것

- 멤버 메서드(멤버 함수)

<br>

### 3. 상속성
---
상위 개념의 특징을 하위 개념이 물려 받는 것
( is a 구조 )

- 상속을 남용하는 것은 좋지 않다.

<br>

### 4. 다형성
---
변수나 함수를 여러 의미로 사용할 수 있는 것

- 오버로딩 : 같은 함수 명을 사용하되, 파라미터(매개변수)의 개수를 달리 하여 사용하는 것

- 오버라이딩 : 부모 클래스에 있는 것을 재정의 하여 사용하는 것

<br>

### 5. 추상성
---
공통 부분(속성이나 기능 등)을 간단하게 추려내는 것

- 추상 클래스
    - 추상 함수 하나를 무조건! 포함하고 있어야 함
    - 객체화가 불가능 함

<br>

## 객체지향 설계 원칙 ( S O L I D )

    - S 단일 책임 원칙 (SRP : Single Responsibility Principle)
    
    - O 개방 폐쇄 원칙 (OCP : Open - Closed Principle)

    - L 리스코프 치환 원칙 (LSP : Liskov Substitution Principle)

    - I 인터페이스 분리 원칙 (ISP : Interface Segregation Principle)

    - D 의존-역전 원칙 (Dependency Inversion Principle)

<br>

### 단일 책임 원칙 (Single Responsibility Principle)
---
작성된 클래스는 하나의 기능만 가지고, 하나의 책임을 수행하는 데 집중해야함

<br>

### 개방 폐쇄 원칙 (Open-Closed Principle)
---
소프트웨어의 구성 요소는 확장(추가)에는 열려있고, 변경(수정)에는 닫혀있어야 함. (확장(추가) O, 변경(수정) X)

확장하는 방식에는 상속과 유니온 방식이 있음.

<br>

### 리스코프 치환 원칙 (Liskov Substitution Principle)
---
서브 타입은 언제나 기반 타입으로 교체할 수 있어야 함

공통 부분은 부모 쪽에 있어야함

<br>

### 인터페이스 분리 원칙 (Interface Segregation Principle)
---
자신이 사용하지 않는 인터페이스는 구현하지 말아야 함

<br>

### 의존 - 역전 원칙 (Dependency Inversion Principle)
---
구조적 디자인에서 발생하던 하위 레벨 모듈의 변경이 상위 레벨 모듈의 변경을 요구하는 위계관계를 끊는 의미의 역전. 실제 사용 관계는 바뀌지 않으며, 추상을 매개로 메시지를 주고 받음으로써 관계를 최대한 느슨하게 만드는 원칙
커플링을 깨기 위해서 콜 지점을 뒤집는 것

<br>

#### <mark>의존성 주입</mark> (DI : Dependency Injection)
---
인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 하는 것