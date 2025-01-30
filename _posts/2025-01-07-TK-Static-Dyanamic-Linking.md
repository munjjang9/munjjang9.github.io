---
layout: post
title: 스태틱 링킹과 다이나믹 링킹
author: munjjang9
tags: [C/C++]
date: 2025-01-07 21:00 +0900
categories: [Languages]
toc: true
---

## Static Linking & Dynamic Linking
---

### Static Linking

- 컴파일 타임에 모든 라이브러리 코드가 실행 파일에 포함된다

- 실행 파일이 독립적으로 실행 가능하다

- Windows의 .lib, Linux의 .a 파일을 사용한다

### Dynamic Linking

- 런타임에 필요한 라이브러리를 로드한다

- 실행 파일에는 라이브러리 참조 정보만 포함된다

- Windows의 .dll, Linux의 .so 파일을 사용한다

<br>

### 차이점
---
<table style="border: 2px;">
  <tr>
    <td> </td>
    <td> Static Linking </td>
    <td> Dynamic Linking </td>
  </tr>

  <tr>
    <td rowspan="3"> 메모리 사용 </td>
  </tr>

  <tr>
    <td> 각 프로그램마다 라이브러리 복사본 필요 </td>
    <td> 여러 프로그램이 하나의 라이브러리 공유 </td>
  </tr>

  <tr>
    <td> 메모리 사용량 증가 </td>
    <td> 메모리 효율적 사용 </td>
  </tr>
  
  <tr>
    <td rowspan="3"> 성능 </td>
  </tr>
  
  <tr>
    <td> 실행 시작 속도 빠름 </td>
    <td> 초기 로딩 시간 필요 </td>
  </tr>
  
  <tr>
    <td> 런타임 오버헤드 없음 </td>
    <td> 함수 호출 시 간접 참조 필요</td>
  </tr>

  <tr>
    <td rowspan="3"> 유지보수 </td>
  </tr>
  
  <tr>
    <td> 라이브러리 업데이트 시 재컴파일 필요 </td>
    <td> 라이브러리만 교체하면 됨 </td>
  </tr>
  
  <tr>
    <td> 배포 크기 큼 </td>
    <td> 배포 크기 작음 </td>
  </tr>
</table>

<br>

### 사용 시점
---

- Static Linking: 독립적인 실행이 필요하거나 성능이 중요한 경우

- Dynamic Linking: 메모리 효율성과 유지보수가 중요한 경우