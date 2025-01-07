---
layout: post
title: 언리얼 엔진 5.3 C++ 포트폴리오(Weapon Action)
author: munjjang9
tags: [Unreal Engine]
date: 2024-12-23 23:00 +0900
categories: [Portfolio]
toc: true
---

# Unreal Engine 5.3 C++ Portfolio Day-8

<iframe width="560" height="315" src="https://www.youtube.com/embed/3AVkCr1MYak?si=EYzJyePadCOq8_7M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

작업 내역

- 콤보 공격

- 적 피격 시 
    - 피격 몽타주 실행
    - 색 변경
    - 히트스탑 적용

- 적 사망 시
    - Collision 비활성화
    - 사망 몽타주 실행
    - 일정 시간 후 Destroy