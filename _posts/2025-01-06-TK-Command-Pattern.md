---
layout: post
title: 커맨드 패턴
author: munjjang9
tags: [C/C++]
date: 2025-01-04 21:00 +0900
categories: [Languages]
toc: true
---

## Command Pattern
---
커맨드 패턴은 객체 지향 디자인 패턴 중 하나로, 요청을 객체의 형태로 캡슐화하여 실행 가능한 작업으로 만드는 패턴이다.

구성 요소

- Command (명령)

    - 요청을 캡슐화하는 인터페이스

    - 일반적으로 execute() 메서드를 포함

- ConcreteCommand (구체적 명령)

    - Command 인터페이스를 구현한 실제 클래스

    - Receiver와 연결되어 실제 요청을 수행

- Receiver (수신자)

    - 실제 작업을 수행하는 객체

    - ConcreteCommand에서 호출되는 실제 동작을 구현

- Invoker (호출자)

    - Command 객체를 저장하고 실행하는 역할

    - 요청을 발신하는 객체

<br>

장점

- 요청을 객체로 캡슐화하여 발신자와 수신자 사이의 의존성을 분리

- 실행 취소(Undo)나 재실행(Redo) 기능 구현 가능

- 요청을 큐에 저장하거나 로그로 기록 가능

단점

- Command 클래스와 ConcreteCommand 클래스가 늘어날수록 코드가 복잡해질 수 있음

- 각 ConcreteCommand 클래스는 실행에 필요한 상태를 유지해야 함