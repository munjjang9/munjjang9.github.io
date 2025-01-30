---
layout: post
title: 유니크 포인터
author: munjjang9
tags: [C/C++]
date: 2025-01-04 21:00 +0900
categories: [Languages]
toc: true
---

## unique_ptr
---

unique_ptr은 C++11에서 도입된 스마트 포인터로, 단일 객체에 대한 독점적인 소유권을 가진다.

<br>

### 소유권 관리
---
- 하나의 객체를 단독으로 소유
- 소유권을 넘길 수는 있지만, 공유는 불가능함
- 복사 생성자와 대입 연산자가 삭제되어 있음(이동만 가능)

<br>

### 메모리 관리
--- 
```cpp
{
  std::unique_ptr<int> ptr(new int(10));
} //블럭을 나오면 자동으로 해제
```

<br>

### 생성 방법
---
```cpp
// 기본 생성
std::unique_ptr<int> ptr1(new int(10));

// 권장 생성 방법(make_unique)
auto ptr2 = std::make_unique<int>(10);
std::unique_ptr<int> ptr2 = std::make_unique<int>(10); //둘이 같은 코드
```

<br>

### 소유권 이전
---
```cpp
std::unique_ptr<int> ptr1 = std::make_unique<int>(10);
std::unique_ptr<int> ptr2 = std::move(ptr1); // 소유권 이전 ptr1 -> ptr2
// ptr1은 이제 nullptr
```

<br>

### 배열 관리
---
```cpp
std::unique_ptr<int[]> arr = std::make_unique<int[]>(5);
arr[0] = 1; // 배열처럼 사용 가능
```

<br>

### 주요 멤버 함수
---
- get()
- release()
- reset()

<br>

#### get()
---
내부 포인터에 직접 접근하는 메서드

```cpp
std::unique_ptr<int> ptr = std::make_unique<int>(10);
int* raw_ptr = ptr.get();
```

<br>

#### release()
---
포인터의 소유권을 반납하고 원시 포인터 반환

```cpp
std::unique_ptr<int> ptr = std::make_unique<int>(10);
int* raw_ptr = ptr.release(); // ptr은 nullptr이 됨
delete raw_ptr; // 수동으로 메모리 해제 필요
```

<br>

#### reset()
---
현재 객체를 삭제하고 새로운 객체로 대체 가능

```cpp
std::unique_ptr<int> ptr = std::make_unique<int>(10);
ptr.reset(new int(20)); // 기존 객체 삭제 후 새로운 객체로 대체
ptr.reset(); // nullptr로 설정
```