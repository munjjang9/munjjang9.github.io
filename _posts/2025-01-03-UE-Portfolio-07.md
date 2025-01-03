---
layout: post
title: 언리얼 엔진 5.3 C++ 포트폴리오 19일차
author: munjjang9
tags: [Unreal Engine]
date: 2025-01-03 23:00 +0900
categories: [Portfolio]
toc: true
---

# Unreal Engine 5.3 C++ Portfolio

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/OayisDgxTzo?si=OfQWacgq7XoFWohn" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

작업 내역

- 적 AI
    - Action

- 문제
    - Action Range와 Approach Range 중간의 애매한 거리가 되면 두 상태를 오가며 Action이 연속해서 수행됨

- 해결 방안
    - Behavior Tree에서 Action 수행 전에 Wait을 두어 공격 빈도를 조절