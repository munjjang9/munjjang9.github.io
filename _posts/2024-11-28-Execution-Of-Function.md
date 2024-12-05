---
layout: post
title:  "함수의 실행"
author: munjjang9
tags: [function]
date: 2024-11-28 15:00 +0900
categories: C/C++
toc: true
---

# 함수의 실행
---
함수를 실행하는 데는 3가지가 필요하다.

**선언부** : 함수를 선언을 하는 부분

**정의부** : 선언한 함수에 대한 정의를 하는 부분

**호출부** : 정의된 함수를 호출하는 부분. 호출이 시작되면 콜 스택(스택 프레임)이 생성됨.

**선언**과 **정의**는 동시에 할 수 있음

<br>

## 예시 1. 선언과 정의를 따로 하는 경우
---
```c
#include <stdio.h>

int Add(int a, int b); //선언부

int main()
{
	int d = Add(10, 20); //호출부 - 콜 스택 생성

	printf("d = %d\n", d);

	return 0;
}

int Add(int a, int b) //정의부
{
	int c = a + b;

	printf("%d + %d = %d\n", a, b, c);

	return c;
}
```

## 예시 2. 선언과 정의를 동시에 하는 경우
---
```c
#include <stdio.h>

int Add(int a, int b) //선언과 동시에 정의
{
	int c = a + b;

	printf("%d + %d = %d\n", a, b, c);

	return c;
}
int main()
{
	int d = Add(10, 20); //호출부 - 콜 스택 생성

	printf("d = %d\n", d);

	return 0;
}
```