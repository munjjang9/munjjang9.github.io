---
layout: post
title: 뷰 행렬
author: munjjang9
tags: [DirectX]
date: 2024-12-27 20:00 +0900
categories: [Game Engine]
toc: true
---

## 뷰 행렬

뷰(View)가 무엇일까? 뷰는 쉽게 말하자면 카메라를 통해 보는 공간이라고 생각하면 된다. 우리는 컴퓨터를 통해 보고 있으니 모니터 상에 나타나는 공간이라고 생각하면 편하다.

View Matrix는 월드 공간 상의 모델의 정점을 뷰 공간으로 변환해주는 행렬이다.

우리의 화면에 표시되기 위해서는 WVP(World-View-Projection)행렬들을 각각 거치게 된다.

WVP 행렬을 행렬곱을 통해 연산을 수행해야 우리의 화면 상에 띄워지게 되는 것이다.

