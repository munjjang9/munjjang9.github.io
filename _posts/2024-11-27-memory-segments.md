---
layout: post
title:  "메모리 할당 영역"
author: munjjang9
tags: [memory segment, code, data, bss, heap, stack]
date: 2024-11-27 20:00 +0900
categories: C/C++
toc: true
---
## 메모리 영역
---
단순히 무언가를 저장하고, 주소를 가지는 것만이 아닌, 영역 별로 여러가지 일을 한다.

메모리 영역의 종류에는 다음과 같은 것들이 있다.
- Code 영역
- Data 영역
- BSS 영역
- Heap 영역
- Stack 영역

영역은 Code -> Data -> BSS -> Heap -> Stack 순서이며, 주소 값은 낮은 값에서 부터 높은 값으로 부여된다.

각 영역은 크게 정적 메모리 영역과 동적 메모리 영역 2가지로 분류 할 수 있다.

---
<br>

## 정적 메모리 영역
---

파일의 사이즈와 관계되어 있음

### Code 영역
---
- 함수 / 상수 저장 (컴파일 단계에서 검사 후, Code 영역에 저장됨)
- 제어문 저장
- 프로그램의 코드를 저장

### Data 영역
---
- 초기화 된 전역 / 정적 변수 저장 (직접 초기화를 하지 않아도 자동 초기화가 되지만, 해주는 것이 가장 좋음)

### BSS 영역
---
- 초기화 되지 않은, 초기화가 0으로 된 전역 / 정적 변수 저장
- 초기화 되지 않은 배열 저장
- 초기화가 Null로 된 포인터 저장

<br>

## 동적 메모리 영역
---

### Stack 영역
---
- 지역 / 매개 변수 저장
- 컴파일에 걸리는 시간 결정

### Heap 영역
---
- 동적 할당 된 변수 저장
- 프로그래머가 유일하게 <ins>직접</ins> 관리할 수 있는 공간

<br>
<br>

## 예문
---
```cpp
int num = 1;                    //Data
int count;                      //BSS

char* str;                      //BSS
const int i = 10;               //Data

int main()
{                               //Stack 생성
    int a, k = 1;               //Stack

    char* ptr;                  //Stack
    ptr = malloc(12);           //Heap

    static int b;               //BSS
    static int c = 2;           //Data

    c = a + b;                  //Code
    k = 3;                      //Code

    func(c, k);                 //Stack

    return 0;
}                               //Stack 소멸

void func(int temp1, int temp2) //Stack
{

}
```