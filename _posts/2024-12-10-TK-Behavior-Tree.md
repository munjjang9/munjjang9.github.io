---
layout: post
title: 비헤이비어 트리
author: munjjang9
tags: [tree]
date: 2024-12-14 22:00 +0900
categories: [Unreal Engine]
toc: true
---

# Behavior tree

<br>

## 비헤이비어 트리란?

AI의 동작의 흐름이나 조건을 제어하기 위해 사용되는 방법으로, 트리 형태로 시각화되어 있다.

## 비헤이비어 트리의 실행 순서

비헤이비어 트리의 실행은 위에서 아래로, 왼쪽에서 오른쪽으로 흘러간다.

## 비헤이비어 트리의 구성 요소

- Root
- Branch (Composites)
    - Selector
    - Sequence
    - Simple Parallel
- Others
    - Tasks (Leaf)
    - Decorators
    - Services

<br>

### Root

---

![Root](/assets/images/BT_Root.png)

루트 노드는 말 그대로 실행의 가장 뿌리가 되는, 실행이 되면 시작하는 노드이다.

<br>

### Composites

---

컴포짓 노드는 각 분기가 실행되는 방식에 대해 규칙을 설정해주는 역할을 하는 노드이다. 컴포짓 노드의 구성 요소로는 셀렉터, 시퀀스, 심플 패러렐 노드가 있다.

<br>

#### Selector

---

![Selector](/assets/images/BT_Selector.png)

셀렉터 노드는 자식 노드를 왼쪽에서부터 오른쪽 순서로 실행시킨다. 만약 실행 중인 자식 노드가 실패하면 다음 노드를 실행시킨다. 반대로, 실행 중인 자식 노드가 성공한다면 다른 자식 노드는 실행되지 않고 종료시킨다.

<br>

#### Sequence

---

![Sequence](/assets/images/BT_Sequence.png)

시퀀스 노드도 자식 노드를 왼쪽에서부터 오른쪽 순서로 실행시킨다. 셀렉터 노드와는 반대로 실행 중인 자식 노드가 실패한다면 다른 자식 노드를 실행하지 않고 종료시킨다. 그리고 성공한다면 다음 노드로 이동해 실행시킨다.

<br>

#### Simple Parallel

---

![Simple Parallel](/assets/images/BT_SimpleParallel.png)

심플 패러렐 노드는 좌측에 연결된  태스크 노드와 우측에 연결된 자식 노드를 동시에 실행시킨다. 적용된 모드에 따라 실행 방식이 달라진다. 좌측에는 태스크 노드만이 연결될 수 있다.

- Immediate 모드 : 메인 태스크 완료 시, 보조 태스크의 실행을 중단시키고 종료시킨다.

- Delayed 모드 : 메인 태스크가 종료되었더라도 보조 태스크가 실행 중이면, 보조 태스크가 종료될 때까지 대기한다.

<br>

### Others

<br>

#### Tasks

---

태스크 노드는 어떤 액션을 취할 지를 나타내는 노드이다.

Wait, Move To와 같은 기본적인 태스크 노드들이 있다.

![Task Nodes Examples](/assets/images/BT_TaskNodes-Example.png)

![Task Nodes](/assets/images/BT_TaskNodes.png)


이 외에도 원하는 기능을 가진 태스크를 직접 만들어 추가할 수 있다.

<br>

#### Decorators

---

데코레이터는 태스크나 컴포짓 노드를 동작하기 위한 조건을 설정해주기 위해 사용한다.

단독으로는 사용할 수 없다.

Blackboard와 Cooldown과 같은 데코레이터들이 있다.

![Decorators Examples](/assets/images/BT_Decorators-Example.png)

![Decorators Examples](/assets/images/BT_Decorators-Example2.png)

위처럼 하나의 노드에 두 개의 데코레이터를 추가하는 것도 가능하다.

![Decorators](/assets/images/BT_Decorators.png)

이런 기본적인 데코레이터들이 존재하고, 태스크 노드와 마찬가지로 원하는 기능을 가진 데코레이터를 직접 만드는 것이 가능하다.

<br>

#### Services

서비스는 블랙보드의 확인과 업데이트에 사용이 된다. 특히 서비스를 이용하여 블랙보드에 설정되어진 키 값을 변경하는 등의 작업을 수행할 수 있다.

![Services Example](/assets/images/BT_Services-Example.png)

위와 같이 하나의 노드에 두 개의 서비스를 추가하는 것이 가능하다.

![Services](/assets/images/BT_Services.png)

이렇게 두 가지의 기본 서비스가 존재하고, 태스크나 데코레이터와 같이 직접 원하는 기능을 담은 서비스를 만들어 사용할 수 있다.