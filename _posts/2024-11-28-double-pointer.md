---
layout: post
title: 이중 포인터
author: munjjang9
tags: [pointer]
date: 2024-11-28 19:10 +0900
categories: [C/C++/C#]
toc: true
---

# 이중 포인터
---
이중 포인터, 이차 포인터, 더블 포인터

포인터 변수는 해당 주소 공간에 있는 값에 접근하기 위해 사용된다.

만약 접근한 주소 공간에 있는 값이 주소라면, 그 때 사용되는 것이 이중 포인터이다.

이중 포인터를 사용한다면,

이중포인터 변수 -> 포인터 변수 -> 값

이런 식으로 접근이 가능하다.

<br>

## 예시
---
```c
int main()
{
	int a = 10;
	int* b = &a; //포인터
	int** c = &b; //이중 포인터

    //아래는 각각 같은 값을 나타낸 것끼리 묶어두었다.

	//a 값
	printf("a = %d\n", a);
	printf("*b = %d\n", *b);
	printf("**c = %d\n", **c);

	printf("\n\n");

	//a 주소
	printf("&a = %p\n", &a);
	printf("b = %p\n", b);
	printf("*c = %p\n", *c);

	printf("\n\n");

	//b 주소
	printf("&b = %p\n", &b);
	printf("c = %p\n", c);

	printf("\n\n");

	//c 주소
	printf("&c = %p\n", &c);

	return 0;
}
```