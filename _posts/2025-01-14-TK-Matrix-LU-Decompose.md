---
layout: post
title: 행렬 LU 분해
author: munjjang9
tags: [Graphics/Rendering]
date: 2025-01-13 21:00 +0900
categories: [Game Development]
toc: true
---

## Matrix LU Decompose
---

LU 분해는 행렬을 두 개의 삼각 행렬(<mark>L</mark>(Lower Triangular Matrix)와 <mark>U</mark>(Upper Triangular Matrix))의 곱으로 표현하는 기법이다. 이는 선형 대수학과 수치 해석에서 중요한 역할을 하며, 주로 선형 방정식의 해를 구하거나 행렬의 역행렬 및 행렬식 계산에 사용된다.

<br>

### 정의
---
LU 분해는 행렬 A를 두 개의 삼각 행렬로 분해됨.

A = L • U

L : 아래 삼각 행렬 (대각선 요소는 1로 고정됨(단위 삼각 행렬))

U : 위 삼각 행렬

<br>

#### 조건
---
- LU 분해는 정사각 행렬(Square Matrix)에 대해 수행됨

- 일부 행렬은 피벗팅(Pivoting)을 통해 LU 분해가 가능. 이는 행렬이 특이하거나 숫자 안정성이 부족한 경우에 필요

<br>

### 알고리즘
---
1. 초기화

2. 상삼각 행렬 U 계산

3. 하삼각 행렬 L 계산

<br>

#### 초기화
---
주어진 행렬 A를 L과 U로 나누기 시작. L과 U는 0으로 초기화

<br>

#### 상삼각 행렬 U 계산
---
