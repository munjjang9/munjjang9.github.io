---
layout: post
title: Check/Verify/Ensure
author: munjjang9
tags: [Unreal Engine]
date: 2024-12-18 22:00 +0900
categories: [Game Engine]
toc: true
---

## Unreal Assert

assert는 예상치 못한 상황을 탐지하는 데 사용되는 키워드이다. 여러가지 조건들을 통해 이를 사전에 방지하는 역할을 한다. 

언리얼 엔진에서는 이와 비슷한 역할을 하는 Check, Verify, Ensure이라는 키워드가 존재한다.

언리얼 엔진은 빌드 모드 등에 따라 DO_CHECK의 숫자가 정의된다.

<br>

### Check

Check는 뒤에 오는 조건식 혹은 파라미터가 false일 경우 하위의 실행을 정지시킨다.

Check(Expression); 처럼 쓰인다.

DO_CHECK가 1인 빌드 시에 실행된다.

<br>

### Verify

Check와 같이 조건식이나 파라미터가 false일 경우 하위의 실행을 정지시킨다.

DO_CHECK가 1일 경우에는 Check와 똑같이 작동한다.

DO_CHECK가 0인 경우에도 실행되며, 변수가 원하는 대로 할당이 되었는지 검증하는 용도로 사용한다.

<br>

### Ensure

보통 치명적이지 않은 오류가 발생할 거라고 예상되는 곳에 사용한다.

Crash Report를 남기지만, 실행을 중지시키지는 않는다.

<br>
<br>
<br>
<br>

- 참고 : https://dev.epicgames.com/documentation/ko-kr/unreal-engine/asserts-in-unreal-engine