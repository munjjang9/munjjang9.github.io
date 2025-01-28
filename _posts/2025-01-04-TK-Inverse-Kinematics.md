---
layout: post
title: IK
author: munjjang9
tags: [Graphics/Rendering]
date: 2025-01-04 21:00 +0900
categories: [Game Development]
toc: true
---

## Inverse Kinematics
---

Inverse Kinematics는 컴퓨터 그래픽스와 게임 개발에서 캐릭터의 관절 움직임을 제어하는 핵심적인 기술이다. 이는 로봇공학, 엔지니어링, 컴퓨터 그래픽스, 비디오 게임 등 다양한 분야에서 활용된다.

<br>

### FK vs IK
---
- Forward Kinematics(FK): 관절의 회전값을 기반으로 최종 위치를 계산하는 방식

- Inverse Kinematics(IK): 목표 위치를 기반으로 관절의 회전값을 역으로 계산하는 방식

<br>

### 장점
---
1. 애니메이터가 각 관절을 일일이 조작할 필요 없이 end-effector의 위치만 지정하면 된다

2. 실시간으로 환경과 상호작용하는 자연스러운 움직임 생성이 가능하다

3. 게임 캐릭터를 물리적으로 게임 월드와 연결하는데 효과적이다
