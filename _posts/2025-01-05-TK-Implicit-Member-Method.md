---
layout: post
title: 암시적 멤버 메서드
author: munjjang9
tags: [C/C++]
date: 2025-01-05 21:00 +0900
categories: [Languages]
toc: true
---

## 암시적 멤버 메서드
---
- 기본 생성자
- 기본 소멸자
- 복사 생성자
- 대입 연산자
- 이동 생성자
- 이동 대입 연산자

<br>

### 기본 생성자
---
- 매개변수가 없는 생성자이다
- 클래스에 다른 생성자가 없을 경우 컴파일러가 자동으로 생성한다
- 객체 멤버와 외부 환경을 초기화하는 역할을 한다

<br>

### 기본 소멸자
---
- 클래스 이름 앞에 ~를 붙여 표시한다
- 객체의 수명이 끝날 때 컴파일러에 의해 자동으로 호출된다
- 사용이 끝난 객체를 정리하는 역할을 한다

<br>

### 복사 생성자
---
- 같은 클래스 타입의 다른 객체를 참조로 받아 자신을 초기화한다
- 깊은 복사(deep copy)를 통해 완전한 독립성을 가진 객체를 생성한다
- 함수에 객체를 전달하거나 반환할 때, 또는 객체로 초기화할 때 호출된다

<br>

### 대입 연산자
---
- 자신과 같은 타입의 다른 객체를 대입받을 때 사용하는 연산자이다
- 기본적으로 얕은 복사(shallow copy)로 수행된다

<br>

### 이동 생성자
---
- Rvalue 참조를 파라미터로 받는 생성자이다
- 얕은 복사 후 원본의 소유권을 이전하고 원본을 NULL로 초기화한다
- 임시 객체를 전달하거나 std::move()를 사용할 때 호출된다

<br>

### 이동 대입 연산자
---
- Rvalue 참조로부터 리소스 소유권을 이전받는다
- 복사 대신 리소스를 이동시켜 성능을 향상시킨다
- 이동 후 원본 객체는 유효하지만 비어있는 상태가 된다

<br>

### 예시
---
```cpp
class MyClass {
public:
    // 기본 생성자
    MyClass() {
        // 멤버 초기화
    }

    // 기본 소멸자
    ~MyClass() {
        // 리소스 정리
    }

    // 복사 생성자
    MyClass(const MyClass& other) {
        // 깊은 복사 구현
    }

    // 대입 연산자
    MyClass& operator=(const MyClass& other) {
        if (this != &other) {  // 자기 대입 검사
            // 깊은 복사 구현
        }
        return *this;
    }

    // 이동 생성자
    MyClass(MyClass&& other) noexcept {
        // 리소스 이동
        // other를 null 상태로 만듦
    }

    // 이동 대입 연산자
    MyClass& operator=(MyClass&& other) noexcept {
        if (this != &other) {  // 자기 대입 검사
            // 기존 리소스 정리
            // 리소스 이동
            // other를 null 상태로 만듦
        }
        return *this;
    }
};
```