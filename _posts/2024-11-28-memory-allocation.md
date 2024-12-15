---
layout: post
title: 메모리 할당
author: munjjang9
tags: [allocation]
date: 2024-11-28 20:00 +0900
categories: [C/C++/C#]
toc: true
---

# 메모리 할당
---
메모리를 언제 할당하느냐에 따라 정적 할당과 동적 할당으로 나뉜다

<br>

## 정적 할당
---
- 컴파일 단계에서 메모리를 미리 할당하는 방법

- [Stack 영역](https://munjjang9.github.io/c/c++/2024/11/27/memory-segments/#stack-%EC%98%81%EC%97%AD)에 할당

- 메모리 공간이 얼마나 필요한 지 항상 알 수 없기에 효율적이지 못함

- 자칫하면 과도하게 메모리가 할당되어 남는 공간이 생길 수가 있음. 또한, 메모리가 필요해져도 추가로 할당 할 수 없음

- 함수가 끝날 시에 할당된 메모리가 자동으로 해제되므로 직접 메모리를 해제하지 않아도 됨

<br>

## 동적 할당
---
- 런타임에서 메모리를 필요할 때마다 할당하는 방법

- [Heap 영역](https://munjjang9.github.io/c/c++/2024/11/27/memory-segments/#heap-%EC%98%81%EC%97%AD)에 할당

- 미리 할당해두는 것이 아니기 때문에 할당해둔 메모리 공간이 부족하거나 남는 현상이 발생하지 않음

- 메모리가 자동으로 해제되지 않기 때문에 메모리를 직접 해제해줘야 함

- 메모리를 해제해주지 않으면 메모리 누수 현상이 발생

- 게임 프로그래밍을 할 때 많이 사용됨

<br>

### 가상 메모리
---
메모리 공간보다 더 많은 주소 공간을 필요로 할 때 사용함

주소 사상 기법(주소 매핑 기법)이라는 기법을 사용함

ex ) 
	
	빈 공간(0x000 ~ 0x100) - a.txt(0x100 ~ 0x200) - 빈 공간(0x200 ~ 0x300) - b.exe(0x300 ~ 0x400)

	이렇게 할당 된 주소 공간이 있다고 가정했을 때, 
	가상 메모리의 주소 매핑은 주소를 연속적으로 사용할 수 있도록
	0x000 ~ 0x100, 0x100 ~ 0x200 으로 매핑이 됨.

<br>

## 예시
---
```c
#include <stdio.h>
#include <Windows.h>

void Allocate_Malloc()
{
	void* p = malloc(20); //20 byte 할당
	int* pi = (int*)p;

	pi[0] = 1;
	*(pi + 1) = 2;

	for (int i = 0; i < 5; i++)
		pi[i] = i + 1;

	for (int i = 0; i < 5; i++)
		printf("pi[%d] = %d\n", i, pi[i]);

	free(p);
}

void Allocate_New()
{
	int* a = new int(); //new는 예약어이자 명령어. 4byte 할당
	*a = 10;
	
	printf("*a = %d\n", *a);

	delete a;
	a = nullptr; //a에 쓰레기 값이 들어가는 걸 방지하기 위함

	int* b = new int[5];
	b[0] = 1;
	*(b + 1) = 2;
	//*b++; //연산자 우선순위가 ++이 높아서 다음 주소로 접근하겠다는 뜻이 됨

	for (int i = 2; i < 5; i++)
		*(b + i) = i + 1;

	for (int i = 0; i < 5; i++)
		printf("b[%d] = %d\n", i, b[i]);

	delete[] b; //배열로 할당된 것은 배열 기호를 붙여줘야 함.
	b = nullptr;
}

struct Matrix
{
	union
	{
		struct  
		{
			float _11, _12, _13, _14;
			float _21, _22, _23, _24;
			float _31, _32, _33, _34;
			float _41, _42, _43, _44;
		};

		float m[4][4];
		float m2[16];
	};
};

void Union()
{
	int count = 0;
	Matrix matrix;

	for (int y = 0; y < 4; y++)
	{
		for (int x = 0; x < 4; x++)
		{
			matrix.m[y][x] = ++count;
		}
	}

	printf("matrix.m[1][2] = %f\n", matrix.m[1][2]);
	printf("matrix.m[1][2] = %f\n", matrix._23);
	printf("matrix.m2[6] = %f\n", matrix.m2[6]);

	printf("%p %p %p\n", &matrix.m[1][2], &matrix._23, &matrix.m2[6]);
}

void Stack_Overflow()
{
	//Matrix matrix[1024][1024];

	//unsigned char a[1024*1009]; //스택 프레임의 크기 약 1MB, 1024 * 1010

	Matrix* matrix = new Matrix[1024 * 1024]; //Heap 구역에 할당되기 때문에 허용 됨
	delete[] matrix;

	matrix = nullptr;
}

void Print_Matrix(Matrix* matrix)
{
	for (int row = 0; row < 4; row++)
	{
		for (int col = 0; col < 4; col++)
		{
			printf("%.0f\t", matrix->m[row][col]); //.0f : 소수점 제거
		}

		printf("\n");
	}

	printf("Matrix Address : %p\n\n", matrix);
}

void Virtual_Alloc()
{
	Matrix* matrix = new Matrix[128];

	int count = 0;

	for (int m = 0; m < 128; m++)
	{
		for (int row = 0; row < 4; row++)
		{
			for (int col = 0; col < 4; col++)
			{
				matrix[m].m[row][col] = count++;
			}
		}
	}

	void* p = VirtualAlloc(nullptr, sizeof(Matrix) * 128, MEM_RESERVE, PAGE_READWRITE);
	 //예약된 공간의 시작 주소를 p에 저장

	for (int i = 0; i < 128; i++)
	{
		void* temp = (BYTE*)p + sizeof(Matrix) * i;

		VirtualAlloc(temp, sizeof(Matrix), MEM_COMMIT, PAGE_READWRITE);
		memcpy_s((BYTE*)temp, sizeof(Matrix), &matrix[i], sizeof(Matrix));
	}

	delete[] matrix;
	matrix = nullptr;

	Print_Matrix((Matrix*)p + 0);
	Print_Matrix((Matrix*)p + 100);

	VirtualFree(p, 0, MEM_RELEASE);
}

int main()
{
	Allocate_Malloc();
	Allocate_New();

	Union();

	Stack_Overflow();

	printf("\n\n");
	Virtual_Alloc();

	return 0;
}
```