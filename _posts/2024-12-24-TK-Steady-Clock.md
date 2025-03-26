---
layout: post
title: steady_clock
author: munjjang9
tags: [C/C++]
date: 2024-12-24 21:00 +0900
categories: [Languages]
toc: true
---

## Steady_Clock과 System_Clock
---
C++에는 시간을 다루기 위한 기능들을 모아둔 chrono라는 라이브러리가 있다.

system_clock과 steady_clock이라는 클래스가 존재한다.

system_clock은 유닉스에서 사용하는 시간인 UTC(1970년 1월 1일 목요일)를 기준으로 그 이후의 시간을 나타낸다. 또한, 사용자가 시스템의 시간을 변경하는 등의 작업으로 인해 system_clock에서 나타내는 시간이 조정될 수 있다. 일반적인 시계를 나타낼 때 쓰인다.

steady_clock은 시스템의 시간과 관련이 있는 것이 아닌 마지막 재부팅 이후의 시간 등, 절대 조정될 수 없는 시간이다. 간격을 측정하기 위해 쓰이는 시계를 나타내는 데 사용된다.

<br>
<br>
<br>
<br>

- 참고 1 : https://en.cppreference.com/w/cpp/chrono/steady_clock
- 참고 2 : https://en.cppreference.com/w/cpp/chrono/system_clock