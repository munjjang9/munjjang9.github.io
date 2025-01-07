---
layout: post
title: 언리얼 엔진 5.3 C++ 포트폴리오(AI Enemy)
author: munjjang9
tags: [Unreal Engine]
date: 2025-01-01 23:00 +0900
categories: [Portfolio]
toc: true
---

# Unreal Engine 5.3 C++ Portfolio Day-17

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/BRQzEruAaUM?si=BSixPA0F4V1Nzpsv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

작업 내역

- 적 AI
    - Patrol
    - Approach

- 문제
    - 적AI가 플레이어를 따라 회전 시 뚝뚝 끊기는 현상 발생

- 해결 방안
    - 보간을 통한 부드러운 회전