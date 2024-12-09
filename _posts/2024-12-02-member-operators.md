---
layout: post
title:  멤버 연산자
author: munjjang9
tags: [operator]
date: 2024-12-02 14:20 +0900
categories: [C/C++]
toc: true
---

# 멤버 연산자
멤버 연산자는 주로 구조체(struct), 공용체(union), 클래스(class) 내의 멤버 또는, 배열에 접근하기 위해 사용한다.

<br>

## 직접 멤버 연산자
직접 멤버 연산자 <mark>.</mark>는 일반적인 멤버에 접근할 때 사용된다.

### 예시
```c
struct Test
{
    int X = 0;
    int Y = 0;
};

int main()
{
    Test t;

    printf("t.X = %d, t.Y = %d\n", t.X, t.Y);

	t.X = 20;
	t.Y = 30;

	printf("t.X = %d, t.Y = %d\n", t.X, t.Y);

    return 0;
}
```

<br>

## 간접 멤버 연산자
간접 멤버 연산자 <mark>-></mark>는 포인터 멤버 연산자로, 포인터로 선언된 것의 멤버에 접근할 때 사용된다.

### 예시
```c
struct Test
{
	int X = 0;
	int Y = 0;
};

int main()
{
	Test* t = new Test();

	printf("%d, %d\n", t->X, t->Y);

	t->X = 20;
	t->Y = 30;

	printf("%d, %d\n", t->X, t->Y);

	delete t;
	t = nullptr;

	return 0;
}
```

## 활용
직접 멤버 연산자와 간접 멤버 연산자의 큰 차이로는 접근 시에 포인터로 접근하느냐 아니냐의 차이라고 볼 수 있다.

그럼 직접 멤버 연산자로는 포인터로 접근할 수 없는가라고 묻는다면, 그렇지 않다.

직접 멤버 연산자인 .도 포인터로 접근이 가능하다.

방법은 간단하다. 우리가 포인터로 접근할 때는 * 연산자를 사용하는데, 이를 활용하면 직접 멤버 연산자로도 포인터 접근이 가능하다.

간단한 예시로 알아보자

### 예시
```c
struct Test
{
	int X = 0;
};

int main()
{
	Test* t = new Test();

	printf("%d\n", t->X);   //0
	printf("%d\n", (*t).X); //0

	t->X = 20; // = (*t).X = 20;

	printf("%d\n", t->X);   //20
	printf("%d\n", (*t).X); //20

	delete t;
	t = nullptr;

	return 0;
}
```