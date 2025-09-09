---
layout: post
title: 아핀 변환
author: munjjang9
tags: [Math]
date: 2024-12-23 21:00 +0900
categories: [Study]
toc: true
---

# Affine Transformation

<br>

## 아핀
---
같은 평면 상에 있는 점들과 그의 평행 이동에 대해 다루는 분야가 아핀 기하학이다.

아핀 변환은 이런 아핀 기하학적 성질들을 보존하는 두 아핀 공간 사이의 함수를 말한다.

아핀 기하학적 성질에는 이동, 팽창, 회전, 전단 등이 있다.

![Translation](/assets/images/Affine-Translation.gif) 
![Dilation](/assets/images/Affine-Dilation.gif)
![Rotation](/assets/images/Affine-Rotation.gif)
![Shear](/assets/images/Affine-Shear.gif)

<br>

이런 변환들은 행렬에 의해 조정되는데, 이 행렬들이 곱해지는 순서가 매우 중요하다. 이 순서가 잘못된다면 원하지 않는 변환이 이루어지기 때문이다.

![Affine Transformation](/assets/images/Affine-Transformation.gif)

위의 그림을 보면 아무렇게나 변환이 이루어지는 것이 아닌, 정해진 순서에 의해 이루어지고 있다.

이 순서에 대해서는 앞 포스트인 [행렬](https://munjjang9.github.io/game%20development/2024/12/22/Matrix/)에서 다루었다.

<br>
<br>
<br>
<br>

- 참고 1 : https://towardsdatascience.com/perspective-versus-affine-transformation-25033cef5766
- 참고 2 : https://towardsdatascience.com/understanding-transformations-in-computer-vision-b001f49a9e61