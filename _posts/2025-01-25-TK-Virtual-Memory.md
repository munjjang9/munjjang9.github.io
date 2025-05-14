---
layout: post
title: 가상 메모리
author: munjjang9
tags: [Operating System]
date: 2025-01-24 21:00 +0900
categories: [Game Development]
toc: true
---

## 가상 메모리
---
가상 메모리는 RAM의 용량에 제약 없이 프로그램이 실행되도록 한다. 실제 메모리의 주소를 할당하는 것이 아닌 가상 메모리의 주소를 할당한다.

<br>

### 가상 메모리의 주소
---
가상 메모리에는 가상 주소와 물리 주소라는 두 가지 개념이 존재한다.

- 가상 주소 : 프로세스가 참조하는 주소. 프로세스마다 독립적으로 할당됨
- 물리 주소 : 실제 메모리의 주소. 하드웨어에서 직접 접근 가능

> CPU가 가상 주소를 통해 메모리에 접근 시, 메모리 관리 유닛(MMU : Memory Management Unit)이 페이지 테이블을 참조하여 가상 주소를 물리 주소로 변환시킴

<br>

### 가상 메모리의 작동
---
1. 프로세스가 실행되면 운영체제에서 프로세스에 가상 주소 공간 할당
2. 프로세스가 특정 가상 주소에 접근을 하려고 하면 MMU가 가상 주소를 물리 주소로 변환해줌
3. 가상 주소에 해당하는 데이터가 물리 메모리에 존재하지 않으면 페이지 폴트 발생
4. 페이지 폴트 발생 시, 운영체제가 해당 데이터를 보조 기억 장치에서 물리 메모리로 가져옴
5. 물리 메모리가 Full이면 페이지 교체 알고리즘에 따라 일부 페이지를 보조 기억 장치로 내보내고 새로운 페이지를 가져옴

<br>

### 요구 페이징(Demand Paging)
---
프로그램 실행 시 필요한 페이지만 메모리에 적재하고 필요하지 않은 페이지는 디스크에 저장하는 기법을 요구 페이징이라고 한다.

필요한 부분만 가져와 사용하는 기법이기에 메모리 사용량을 줄일 수 있고 I/O 오버헤드를 줄일 수 있다.

<br>

### 페이지 폴트
---
CPU가 접근하려는 페이지가 메모리에 없는 경우에 발생한다. 이 경우에 OS에서 해당 페이지를 SSD나 HDD와 같은 보조 기억 장치에서 찾아 이를 메모리에 적재시킨다.

<br>

#### 페이지 폴트 과정
---
1. 메모리 관리 장치(MMU)가 페이지 폴트 트랩을 발생시킴

2. OS가 페이지 테이블에서 해당 페이지가 존재하는 위치를 확인

3. 해당 페이지를 보조 기억 장치에서 찾아 메모리에 적재

4. 페이지 테이블 갱신

5. 중단된 명령 재실행

<br>

### 페이지 교체
---
메모리가 가득 찬 경우, 가져올 페이지를 어떤 페이지와 교체할 지를 결정하는 방법이다. 이를 통해 페이지 부재율을 줄여 시스템의 성능을 향상시킨다.

<br>

### 페이지 교체 알고리즘
---
- FIFO(First In First Out)
    - 메모리에 가장 먼저 들어온 페이지를 우선적으로 교체하는 알고리즘
![First In First Out](/assets/images/PageReplacement_FIFO.png)

- LRU(Least Recently Used)
    - 가장 오랜 시간동안 사용되지 않은 페이지를 우선적으로 교체하는 알고리즘
![Least Recently Used](/assets/images/PageReplacement_LRU.png)

- OPT(Optimal)
    - 앞으로 사용량이 가장 적을 페이지를 우선적으로 교체하는 알고리즘(구현이 어려움)
![Optimal](/assets/images/PageReplacement_OPT.png)

- LFU(Least Frequently Used)
    - 참조 횟수가 가장 적은 페이지를 우선적으로 교체하는 알고리즘
![Least Frequently Used](/assets/images/PageReplacement_LFU.png)

- MFU(Most Frequently Used)
    - 참조 횟수가 가장 많은 페이지를 우선적으로 교체하는 알고리즘(많이 사용되었으니 사용되지 않을거라 판단하는 경우)
![Most Frequently Used](/assets/images/PageReplacement_MFU.png)

- NUR(Not Used Recently)
    - 최근에 사용되지 않았던 페이지를 우선적으로 교체하는 알고리즘
![Not Used Recently]()

