---
layout: post
title: GUID & UUID
author: munjjang9
tags: [Software Engineering]
date: 2025-01-15 21:00 +0900
categories: [Game Development]
toc: true
---

## GUID & UUID
---
GUID와 UUID는 둘 다 기본적으로 고유 식별자를 만들어 관리하기 위해 사용된다.

그렇다면 왜 GUID와 UUID로 나누어져 있고, 이 둘은 어떻게 다를까?

<br>

### GUID(Globally Unique Identifier)
---
GUID는 우선 마이크로소프트에서 사용하는 식별자이다.

Windows 환경이나 닷넷 프레임워크에서 활용된다.

<br>

### UUID(Universally Unique Identifier)
---
UUID는 국제 표준으로 지정된 식별자이다.

그렇기에 리눅스나 맥OS 등 여러 플랫폼에서 사용된다.

<br>

### 공통점
---
GUID와 UUID는 둘 다 고유 식별자로 관리하는 방식이기에 여러가지 공통점이 있다.

1. 128비트 체제
    - 32자리의 16진수 숫자를 사용한다
2. 분할 방식
    - 32자리를 5개의 그룹으로 분할함. 8-4-4-4-12 자리씩 분할

<br>

### 차이점
---
<table style="border: 2px;">
  <tr>
    <td> 구분 </td>
    <td> GUID </td>
    <td> UUID </td>
  </tr>

  <tr>
    <td> 용어 기원 </td>
    <td> Microsoft </td>
    <td> IETF RFC 4122 표준 </td>
  </tr>

  <tr>
    <td> 표기 방식 </td>
    <td> 대문자 권장 </td>
    <td> 대소문자 구분X </td>
  </tr>

  <tr>
    <td> 주요 사용처 </td>
    <td> 윈도우, 닷넷 </td>
    <td> 마이크로소프트 환경을 제외한 플랫폼 </td>
  </tr>
</table>

