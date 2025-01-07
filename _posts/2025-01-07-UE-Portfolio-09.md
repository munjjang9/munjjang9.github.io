---
layout: post
title: 언리얼 엔진 5.3 C++ 포트폴리오(Enemy Combo)
author: munjjang9
tags: [Unreal Engine]
date: 2025-01-07 20:00 +0900
categories: [Portfolio]
toc: true
---

# Unreal Engine 5.3 C++ Portfolio Day-24

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/77-ASVBNwSs?si=vU22HwzFm5r35AX9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

작업 내역

- 적 Combo
    - Player처럼 원할 때 입력을 받을 수 없기에 따로 공격 명령을 내려줘서 처리해야 함

- 문제
    - Player 피격 시 State가 꼬여서 무기 장착 등의 동작이 수행되지 않음
    - Player와 Enemy 사이의 거리 때문에 Combo가 원활하게 수행되지 않음

- 해결 방안
    - 피격 후의 State 처리 예정정
    - 임시로 Enemy의 공격에 밀어내는 거리를 0으로 줌.