---
layout: post
title: 구면좌표계
author: munjjang9
tags: [Math]
date: 2024-12-22 21:00 +0900
categories: [Game Development]
toc: true
---

## Sphere Coordinate System

구면 좌표계는 3차원 공간 상에 점들을 나타내는 좌표계 중 하나이다.

3D 극좌표계와 많이 이야기된다.

구면 좌표계는 하나의 물체를 기준으로 궤도 형식으로 도는 물체 등을 구현할 때 자주 쓰인다.

![Spherical Coordinate](/assets/images/Spherical-Coordinate.gif)

이때 점 P의 좌표는 P(r, θ, Φ)가 된다.

<br>

### 구면 - 직교 변환

![Sphere Coordinate System transformation](/assets/images/Sphere-Coordinate-System-transformation.png)

둘 간의 변환은 이런 식으로 이루어진다.

여기서 각 좌표는 다음을 나타낸다.

    r : 구의 중심(O)으로부터 점 P까지의 거리

    θ : Z축과 직선 OP가 이루는 양의 각

    Φ : 직선 OP를 XY 평면에 투영시킨 직선과 X축이 이루는 양의 각

구면 좌표계에서는 한 점에 대한 표현이 여러 가지가 나올 수가 있기 때문에 보통 각 좌표의 범위를 제한한다.



