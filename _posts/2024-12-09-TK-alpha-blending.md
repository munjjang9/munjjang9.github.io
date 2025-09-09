---
layout: post
title: 알파 블렌딩
author: munjjang9
tags: [Graphics/Rendering]
date: 2024-12-9 23:59 +0900
categories: [Study]
toc: true
---

## 알파 블렌딩( Alpha Blending )

이미지와 이미지를 합성할 때에, RGB 색상이 아닌 투명도(알파) 값을 적용하여 자연스러운 합성을 하기 위한 기술이라고 볼 수 있다.

![알파 블렌딩](/assets/images/AlphaBlending.png)

알파 값은 표현하는 방식에 따라 0 ~ 255 또는 0 ~ 1 로 나타낸다.

알파 값을 0 ~ 1로 나타낸다고 했을 때, 알파 블렌딩 공식은 다음과 같다

**결과 = 원본 색 * 원본 알파 값 + 합성될 색 * (1 - 합성될 알파 값)**

<br>

---
###### 참조 : https://trts1004.tistory.com/12109286