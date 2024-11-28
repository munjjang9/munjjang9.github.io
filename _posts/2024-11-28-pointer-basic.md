---
layout: post
title:  "포인터 기초"
author: munjjang9
tags: [c, cpp]
date: 2024-11-28 13:00 +0900
categories: C/C++
toc: true
---
## 포인터란?
---
어떠한 변수 등의 주소를 가리키기 위해 사용되는 것으로, 해당 주소에 접근하고 사용하기 위하여 쓰인다.

## 포인터 사용
---
포인터는 주로 변수 등의 이름 앞에 <mark>*</mark> 기호를 붙여 사용한다

포인터 변수에 어떠한 변수의 주소를 저장할 때는 변수 앞에 <mark>&</mark> 기호를 붙여 사용한다

## 예시
---
```C++
#include <stdio.h>

int main()
{
	int a = 10;
	printf("a = %d\n", a);
	printf("&a = %p\n", &a);

	int* p = &a; //정수형 포인터 변수 p에 a의 주소 값 대입
	printf("p = %p\n", p); //a의 주소 값
	printf("*p = %d\n", *p); //a의 값 10
	printf("&p = %p\n", &p); //p의 주소 값

	*p = 20; //p가 가리키는 주소 내의 값을 바꿈
	printf("*p = %d\n", *p); //바뀐 a의 값인 20
	printf("a = %d\n", a); //20

	//주소의 크기는 x86환경에서는 4바이트, x64환경에서는 8바이트

	int& r = a; //a의 주소에 r이라는 이름을 붙임, r과 a는 동일한 주소를 가리키게 됨

	printf("a = %d\n", a);
	printf("r = %d\n", r);
	printf("&a = %p\n", &a);
	printf("&r = %p\n", &r);

	return 0;
}
```
