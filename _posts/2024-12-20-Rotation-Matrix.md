---
layout: post
title: 회전 행렬
author: munjjang9
tags: [Math]
date: 2024-12-20 23:00 +0900
categories: [Study]
toc: true
---

# Rotation Matrix

<br>

## 회전 행렬 유도 과정

DirectX를 공부하던 중, 회전 행렬에 대해 접하게 됐는데, 언리얼 엔진도 그렇고 이미 구현된 회전 행렬을 사용했기에 회전 행렬에 대한 이해도가 떨어졌다.

DirectX를 이용한 프로그래밍을 시작하며 회전 행렬을 이해해 보고자 직접 회전 행렬을 유도해 보았다.

게임 프로그래밍에 있어 회전은 3가지로 나뉜다.

1. Pitch 회전

2. Yaw 회전

3. Roll 회전

<br>

---

이제부터 유도할 회전 행렬은 왼손 좌표계에 DirectX의 축을 기준으로 진행하고자 한다.

<br>

### Pitch 회전
---
DirectX 기준, Pitch 회전은 X축을 기준으로 한 회전이다.

왼손 좌표계가 기준이기에, 축을 기준으로 반시계 방향 회전을 시킨다.

X축이 기준이기에, 회전이 일어나는 평면은 Y-Z 평면이 된다.

이해를 쉽게 하기 위해 각 축의 1이 되는 지점을 향하는 벡터를 기준으로 설명하고자 한다.

그림으로 표현해 보자면 다음과 같다.

![Pitch Rotation](/assets/images/PitchRotation.png)

<br>

각 벡터를 성분으로 분해한 후, 선형변환을 하여 회전 후의 벡터를 알아내 보겠다.

빨간 실선이 회전 후의 벡터인데, 이 벡터의 성분을 알아내기 위해서는 사인과 코사인을 이용할 것이다.

회전 값이 θ라고 할 때, Y축에서 회전된 벡터의 성분을 좌표로 나타내면 (0, cosθ, sinθ)가 된다.

유도 공식은 다음과 같다.

![Pitch Rotation Induction](/assets/images/PitchRotation-Matrix-Induction.jpeg)

<br>

### Yaw 회전

Yaw 회전은 Y축을 기준으로 한 회전이다.

당연히 왼손 좌표계이고, Y축을 기준으로 반시계 방향 회전을 시킨다.

Y축이 기준이기에, 회전이 일어나는 평면은 <mark>Z-X</mark> 평면이 된다. 

X-Z 평면이 아니고 Z-X 평면이다. 이게 중요한 포인트 중 하나이다.

왼손을 열심히 돌려가며 보다보면 왜 Z-X 평면인지 새삼 깨닫게 될 것이다(경험담이다).

회전과 좌표를 그림으로 그려보면 다음과 같다.

![Yaw Rotation](/assets/images/YawRotation.png)

유도 과정은 Pitch 회전과 비슷하다.

바로 유도 과정으로 넘어가보자.

![Yaw Rotation Induction](/assets/images/YawRotation-Matrix-Induction.jpeg)

<br>

### Roll 회전

Roll 회전은 Z축을 기준으로 한 회전이다.

동일하게 왼손 좌표계에 Z축을 기준으로 반시계 방향 회전이 일어난다.

Z축이 기준이기에 X-Y 평면에서 회전이 일어난다.

다음은 회전이 일어나는 평면을 그림으로 그린 것이다.

![Roll Rotation](/assets/images/RollRotation.png)

유도 과정은 다음과 같다.

![Roll Rotation Induction](/assets/images/RollRotation-Matrix-Induction.jpeg)

<br>
<br>
<br>

보통 사용하는 변환 행렬은 4 * 4 행렬이지만, 이번 포스트는 회전 행렬에 중점을 두었다.

3차원 회전은 3 * 3 행렬에서 이루어지기 때문에 3 * 3 행렬을 가지고 회전 식을 유도해보았다.

직접 그려보고 식을 유도하다보니 회전 행렬을 다루는 것에 대한 이해가 조금은 깊어진 것 같았고, 몇 번의 시행착오 끝에 회전 행렬에서 중요한 것을 깨달았다.

내 개인적인 생각으로 회전 행렬 식을 유도하는 데 가장 중요한 것은 <mark>축 정렬</mark>이었다.

축이 정렬되지 않은 채 무작정 행렬 식을 유도하면 의도하지 않은 전혀 다른 회전 값이 나오기 때문이다.

<br>
<br>
<br>
<br>
<br>
<br>

- 참조 : https://ko.khanacademy.org/