---
layout: post
title:  "이중 포인터 2"
author: munjjang9
tags: [pointer]
date: 2024-11-29 17:00 +0900
categories: C/C++
toc: true
---

```c
#include <stdio.h>

void Create(int* value)                 //int* value = obj(nullptr)
{
	value = new int();
	*value = 10;                    //value = 10
}                                       //스택 소멸

int main()
{
	int* obj = nullptr;             //obj = nullptr

	Create(obj);
	printf("*obj = %d\n", *obj);    //10 안 나오고 에러남 obj = nullptr

	delete obj;

	return 0;
}
```

```c
void Create(int** value)            //int** value = &obj
{
	*value = new int();
                                    //힙 공간 생성 *value == obj = 힙 공간의 주소 전달
	**value = 10;               //힙 공간의 주소에 접근해 10 저장
}                                   //스택 소멸

int main()
{
	int* obj = nullptr;         //obj = nullptr

	Create(&obj);
	printf("*obj = %d\n", *obj);//10

	delete obj;
	obj = nullptr;

	return 0;
}
```