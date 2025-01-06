---
layout: post
title: 언리얼 엔진 5.3 C++ 포트폴리오 22일차
author: munjjang9
tags: [Unreal Engine]
date: 2025-01-06 08:00 +0900
categories: [Portfolio]
toc: true
---

# Unreal Engine 5.3 C++ Portfolio

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/ORZ-L-4Wafg?si=nDkKlo5ion8gAiC2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

작업 내역

- Widget
    - Player
    - Enemy

- 문제
    - Enemy Widget이 Enemy의 Collision 하위에 있어서 Enemy가 사망 모션에 들어가도 계속 피격이 되는 현상 발생

- 해결 방안
    - Enemy가 사망 상태에 돌입할 때 Widget을 먼저 삭제.(Widget이 붙는 곳을 변경해볼까 고민중)