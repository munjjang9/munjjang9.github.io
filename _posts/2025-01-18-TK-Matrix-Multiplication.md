---
layout: post
title: 행렬 곱
author: munjjang9
tags: [Math]
date: 2025-01-17 21:00 +0900
categories: [Game Development]
toc: true
---

## Matrix Multiplication
---
두 개의 행렬을 곱하여 새로운 행렬을 생성하는 연산이다.

m x n 크기의 행렬 A, n x p 크기의 행렬 B가 있을 때, 이 둘을 곱하면 m x p 크기의 행렬인 C가 생성된다.

컴퓨터 그래픽스에서는 모델링과 렌더링에 사용되고, 카메라 변환과 물체 변환 등이 행렬곱을 통해 수행된다.

<br>

### 행렬곱 조건과 특징
---
행렬을 곱할 때는 충족되어야만 하는 조건이 있다.

바로 앞 행렬의 열의 수와 뒷 행렬의 행의 수가 같아야 한다는 것이다.

위에서 얘기했듯, m x n 크기의 행렬과 n x p 크기의 행렬이 있다고 했을 때, 

앞의 행렬의 열은 n, 뒷 행렬의 행은 n으로 동일하므로 서로 곱 연산이 가능하다.

이럴 때 행렬곱을 통해 m x p 행렬을 구할 수 있는 것이다.

![행렬A](/assets/images/MatrixMultiplication_A.png) 와 ![행렬B](/assets/images/MatrixMultiplication_B.png)를 곱하면
![행렬AxB](/assets/images/MatrixMultiplication_AXB.png)
![행렬Result](/assets/images/MatrixMultiplication_Result.png)

이런 결과물이 나오게 된다.