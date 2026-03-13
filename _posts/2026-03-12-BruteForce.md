---
layout: post
title: "완전탐색 (Brute Force)"
author: munjjang9
tags: [Algorithm, BruteForce, C++]
date: 2026-03-12 21:00 +0900
categories: [Algorithm]
toc: true
---

## 전날 내용 요약 — 정렬 (Sort)

- `std::sort`: 평균 O(N log N) 인트로소트 (퀵소트+힙소트+삽입소트 하이브리드)
- 커스텀 비교 함수 작성 시 Strict Weak Ordering 준수 — 같은 원소끼리는 반드시 `false` 반환
- 다중 정렬 기준: `if (a.x != b.x) return ...; return ...;` 패턴
- `stable_sort`: 동일 원소의 원래 순서 보장, O(N log² N)

---

## 완전탐색이란?

가능한 모든 경우의 수를 다 시도해서 정답을 찾는 방법이다.  

복잡한 최적화를 거치지 않아도 정답을 보장하며, 입력 크기가 작은 경우에는 항상 유효한 선택지가 된다.  

시간복잡도를 계산해서 통과가 가능하다면 다른 복잡한 알고리즘을 쓰는 것보다 완전탐색으로 풀 수 있는지 확인하는 전략을 취하는 것이 좋다.  

---

## 기본 반복문 완전탐색

배열에서 두 수의 합이 target인 쌍을 찾는 방법을 예시로 들었다.
```cpp
int n = v.size();
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        if (v[i] + v[j] == target) {
            // 찾음
        }
    }
}
```

이 경우, 시간복잡도는 O(n²)이며, n이 10,000이하인 경우 1초 안에 통과가 가능하다.

---

## 순열 — next_permutation

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {1, 2, 3};

// 반드시 오름차순 정렬 후 시작해야 모든 순열을 얻을 수 있다.
sort(v.begin(), v.end());

do {
    for (int x : v) cout << x << " ";
    cout << "\n";
} while (next_permutation(v.begin(), v.end()));
```

경우의 수는 n!이다.

이 경우에는 시간복잡도가 O(n * n!)이므로, n이 8~9 이하인 경우에만 통과가 가능하다.

---

## 조합 — 재귀 구현

```cpp
void combination(vector<int>& nums, int r, int start) {
    if ((int)chosen.size() == r) {
        for (int x : chosen) cout << x << " ";
        cout << "\n";
        return;
    }

    for (int i = start; i < (int)nums.size(); i++) {
        chosen.push_back(nums[i]);
        combination(nums, r, i + 1);
        chosen.pop_back();
    }
}
```

start 파라미터에 i+1이 전달되면서 항상 현재 선택한 원소보다 뒤에 있는 원소만을 선택 가능하게 한다. 이 덕분에 다른 중복 조합이 생기지 않는다.

---

## 부분집합 — 비트마스크

n개의 원소로 만들 수 있는 모든 부분집합을 열거하는 방식이다.

```cpp
vector<int> v = {1, 2, 3};
int n = v.size();

for (int mask = 0; mask < (1 << n); mask++) {
    cout << "{ ";
    for (int i = 0; i < n; i++) {
        if (mask & (1 << i)) { //i번째 비트가 1이면
            cout << v[i] << " ";
        }
    }
    cout << "}\n";
}
```

이 경우에는 O(n * 2^n)정도의 시간복잡도를 가지기 때문에 n이 20이하인 경우에는 안전하게 통과가 가능하다.

---

## 시간복잡도 정리

| 유형 | 경우의 수 | N의 실용적 한계 |
|---|---|---|
| 순열 (N!) | N! | N ≤ 8 (40,320) |
| 조합 C(N,R) | N! / R!(N-R)! | N ≤ 25 수준 |
| 부분집합 (2^N) | 2^N | N ≤ 20 (1,048,576) |
| 이중 반복문 (N²) | N² | N ≤ 10,000 |

---

## 완전탐색 풀이 전략

1. n의 크기를 먼저 확인한다.(시간복잡도 계산)
2. 유형을 분류한다
    - 순서O -> 순열
    - 순서X -> 조합(재귀)
    - 선택/미선택 -> 부분집합(비트마스크)
    - 격자 탐색 -> DFS/BFS
3. Pruning(불필요한 탐색 조기 종료)
