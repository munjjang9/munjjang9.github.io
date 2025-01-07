---
layout: post
title: 언리얼 엔진 5.3 C++ 포트폴리오(Targeting Movement)
author: munjjang9
tags: [Unreal Engine]
date: 2024-12-26 23:00 +0900
categories: [Portfolio]
toc: true
---

# Unreal Engine 5.3 C++ Portfolio Day-12

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/OayisDgxTzo?si=OfQWacgq7XoFWohn" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

작업 내역

- 타겟팅
    - Targeting 중일 경우, bUseControlRotationYaw true, bOrientRotationToMovement false
    - Targeting 중이 아닐 경우, 반대로 적용
    - 각 경우 다른 이동 애니메이션 적용

- 기타
    - 무기 Sword->Katana 변경

- 문제
    - 타겟팅 중 옆으로 움직이면 적과의 거리가 점점 벌어짐(해결방안 모색 중)