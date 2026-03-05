---
layout: post
title: 시간복잡도 (Time Complexity)
author: munjjang9
tags: [Algorithm, CS]
date: 2026-03-05 18:25 +0900
categories: [Study]
toc: true
---

## 시간복잡도란?
---
코드가 동작할 때 연산 횟수가 증가하는 비율의 척도



<br>

## 빅오 표기법 (Big-O Notation)
---
입력의 크기가 n만큼 커질 때 연산을 하는 횟수가 얼마나 늘어나는지를 표현하는 방법



<br>

### O(1) — 상수 시간
---
단계 수가 변하지 않음.
데이터의 증가가 알고리즘에 영향을 주지 않음


예) 배열에서 특정 인덱스 값에 접근하는 것.

```cpp
int Find(vector<int>& v, int index)
{
    return v[index];
}
```

<br>

### O(n) — 선형 시간
---
n번의 반복을 수행.
데이터의 증가가 알고리즘에 영향을 미침


예) 하나의 반복문

```cpp
for(int i = 0; i < n; i++)
{
    수행할 코드
}
```

<br>

### O(n²) — 이차 시간
---
n번의 반복을 n번 수행하는 것. 예) 이중 반복문



```cpp
for(int i = 0; i < n; i++)
{
    for(int j = 0; j < n; j++)
    {
        수행할 코드
    }
}
```

<br>

### O(log n) — 로그 시간
---
데이터가 두 배로 늘어나면 단계가 한 단계씩 증가.


예) 이진 탐색
```cpp
int low = 0;
int high = n - 1;
while(low <= high)
{
    int mid = (low + high) / 2;
    if(arr[mid] == key) return mid;
    else if(arr[mid] > key) high = mid - 1;
    else low = mid + 1;
}
```

<br>

## n 크기별 허용 복잡도
---
이 표에서 대략적으로 확인할 수 있듯이, n의 크기 별로 사용하기 좋은 알고리즘을 역산해볼 수 있다.

| n의 크기 | 가능한 복잡도 |
|----------|---------------|
| n ≤ 10 | O(n!), O(2ⁿ) |
| n ≤ 20 | O(2ⁿ) |
| n ≤ 500 | O(n³) |
| n ≤ 3,000 | O(n²) |
| n ≤ 100,000 | O(n log n) |
| n ≤ 1,000,000 | O(n) |
| n ≤ 10,000,000 | O(log n), O(1) |


<br>

## 마치며
---
효율적인 코드를 짜는 것의 시작은 시간 복잡도를 아는 것부터 라고 생각된다.

