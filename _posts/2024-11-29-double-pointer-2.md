---
layout: post
title:  "이중 포인터 2"
author: munjjang9
tags: [pointer]
date: 2024-11-29 17:00 +0900
categories: C/C++
toc: true
---

# 이중 포인터 2
[이중 포인터](https://munjjang9.github.io/c/c++/2024/11/28/double-pointer/)

이중 포인터는 생성 패턴으로 많이 사용되곤 한다.


## 잘못된 예시
---
value가 obj와 같이 null 값을 가지고 Create 함수가 실행되면서 힙 공간의 주소를 할당 받아 그 공간에 10이라는 값을 저장하게 됨.

Create 함수가 종료되면 콜 되었던 스택이 소멸되고, obj는 값의 변화가 없어 null 값을 가진 채로 printf를 만나 에러가 발생하게 된다.
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

## 해결 예시
---
위의 문제는 이중포인터로 해결할 수 있다.

아까처럼 **value에 obj의 값인 nullptr을 받아오는 것이 아닌, obj 자체의 주소 (&obj) 를 받아온다.

그렇게 되면, value에는 obj의 주소 값이, obj에는 새로 생성된 힙 공간의 주소 값이 들어가게 된다.

따라서 Create 함수의 콜 스택이 소멸되어도 value에서 obj의 주소를 가리키던 것이 끊어질 뿐, obj가 가리키던 힙의 공간이 사라지는 것은 아니기에 10이라는 값이 남아있게 된다.

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