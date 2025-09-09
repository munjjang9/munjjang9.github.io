---
layout: post
title: 워치독 타이머
author: munjjang9
tags: [Embedded System]
date: 2024-12-15 22:00 +0900
categories: [Study]
toc: true
---

# WatchDog Timer

<br>

## 워치독 타이머
---
> 컴퓨터의 오작동을 탐지하고 복구하는데 쓰이는 전자 타이머

설정된 일정 간격마다 MCU(Micro Controller Unit)와 통신하며 MCU가 비정상적인 행동(Kick이 없으면)을 보일 때 MCU에 리셋 신호를 보낸다.

![WatchDog-Timer](/assets/images/WatchDog_Timer.png)

<br>

### 워치독 타이머 사용 이유
---
컴퓨터의 오작동 탐지와 복구에 전자 타이머를 왜 사용할까? 컴퓨터가 고장나면 보통은 수리를 하거나, 어디 수리 업체에 맡기거나 한다. 

하지만 그럴 수 없는 컴퓨터라면 어떻게 해야할까? 이럴 때 사용하는 것이 워치독 타이머이다. 사람이 쉽게 접근할 수 없는 곳에 있는 컴퓨터 같은 경우에 많이 사용된다. 예시로 인공위성이나 탐사선 등이 있다.

<br>

### 워치독 타이머의 구성요소
---
- Clock : CPU와 Timer 사이에서 동작. Kick이 발생한 후의 TimeOut 카운트 다운을 실행
- Clear : Kick이 정상적으로 들어오고 있는지를 확인
- TimeOut : Timer에 예정된 동작을 실행하기 위해 설정된 시간
- Reset : 컴퓨터를 다시 시작하게하는 신호

<br>

워치독 타이머는 위치에 따라 외부 워치독 타이머와 내부 워치독 타이머로 나뉨
