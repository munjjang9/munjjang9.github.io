---
layout: post
title: 컴퓨터에서의 수 표현
author: munjjang9
tags: [Network]
date: 2025-01-21 21:00 +0900
categories: [Game Development]
toc: true
---

## 컴퓨터에서의 수 표현
---
컴퓨터에서는 2진수로 수를 표현한다. 이는 오류를 최소화하고 비용과 시간을 절약하기 위함이다.

<br>

### 정수형의 표현
---
<table style="border: 2px;">

  <tr>
    <td> 크기 </td>
    <td> 바이트 </td>
    <td> 부호 여부 </td>
    <td> 범위 </td>
    <td> 어셈블리 자료형 </td>
    <td> C언어 자료형 </td>
  </tr>
  
  <tr>
    <td rowspan = "3"> 8 비트 </td>
    <td rowspan = "3"> 1 바이트 </td>
  </tr>
  <tr>
    <td> 없음 </td>
    <td> 0 ~ 2<sup>8</sup> - 1 </td>
    <td> BYTE </td>
    <td> unsigned char </td>
  </tr>
  <tr>
    <td> 있음 </td>
    <td> -2<sup>7</sup> ~ 2<sup>7</sup> - 1 </td>
    <td> SBYTE </td>
    <td> char </td>
  </tr>

  <tr>
    <td rowspan = "3"> 16 비트 </td>
    <td rowspan = "3"> 2 바이트 </td>
  </tr>
  <tr>
    <td> 없음 </td>
    <td> 0 ~ 2<sup>16</sup> - 1 </td>
    <td> WORD </td>
    <td> unsigned short </td>
  </tr>
  <tr>
    <td> 있음 </td>
    <td> -2<sup>15</sup> ~ 2<sup>15</sup> - 1 </td>
    <td> SWORD </td>
    <td> short </td>
  </tr>

  <tr>
    <td rowspan = "3"> 32 비트 </td>
    <td rowspan = "3"> 4 바이트 </td>
  </tr>
  <tr>
    <td> 없음 </td>
    <td> 0 ~ 2<sup>32</sup> - 1 </td>
    <td> DWORD </td>
    <td> unsigned int </td>
  </tr>
  <tr>
    <td> 있음 </td>
    <td> -2<sup>31</sup> ~ 2<sup>31</sup> - 1 </td>
    <td> SDWORD </td>
    <td> int </td>
  </tr>

  <tr>
    <td rowspan = "3"> 64 비트 </td>
    <td rowspan = "3"> 8 바이트 </td>
  </tr>
  <tr>
    <td> 없음 </td>
    <td> 0 ~ 2<sup>64</sup> - 1 </td>
    <td> QWORD </td>
    <td> unsigned long <br>(unsinged long long) </td>
  </tr>
  <tr>
    <td> 있음 </td>
    <td> -2<sup>63</sup> ~ 2<sup>63</sup> - 1 </td>
    <td> SQWORD </td>
    <td> long <br> (long long) </td>
  </tr>
  
</table>

<br>

### 음수의 표현
---
32개의 비트 중 가장 앞에 위치한 비트를 부호 비트로 배정하고, 이 비트가 0이면 양수, 1이면 음수로 나타낸다.

음수를 표현하는 대표적인 3가지 방법이 있다.

- 부호화 절대치

- 1의 보수 방법

- 2의 보수 방법

<br>

#### 부호화 절대치
---
부호 비트를 제외한 나머지 비트들을 숫자로써 표현하고, 부호 비트를 통해 양수/음수 여부를 판별하는 방법이다.

예를 들어 00000111 과 10000111이 있을 때,
00000111은 7을 나타내고, 10000111은 -7을 나타낸다.

이 방법의 문제점은 음수와 양수간의 덧셈에서 찾아볼 수 있다.

00000111과 10000111을 더한다고 했을 때, 우리는 7과 -7을 더하면 0이라는 사실을 알고 있다.
하지만 이를 연산하게 되면 10001110으로 -14가 나오게 된다.

<br>

#### 1의 보수 방법
---
1의 보수 방법은 양수로 표현된 비트를 반전시켜 음수를 표현하는 방법이다.

예를 들어 00000111(7)이 있으면 이를 반전시켜 11111000(-7)을 표현하는 것이다.

1의 보수 방법에 대한 정의는 다음과 같다.

> 총 n개의 비트로 정수를 표현할 때, 모든 n비트가 1로 이루어진 수 (2<sup>n</sup> - 1 = 111...11<sub>(2)</sub>)에서 표현하고 싶은 음수의 절댓값을 뺀 수가 바로 1의 보수 방법으로 표현한 음수가 된다.

결국 11111111 - 00000111이나 00000111을 반전시켜 만든 수나 모두 11111000으로 같다.

이런 1의 보수 방법에도 문제점이 존재한다.

00000000으로 표현되는 +0과 11111111로 표현되는 -0이 있다는 점인데, 우리의 관점에서 +0이나 -0은 같은 0이지만, 컴퓨터의 입장에서는 +0과 -0은 다른 수로 분류된다는 것이다.

그렇기에 11111000 과 00000111을 연산하면 -7 + 7이기에 0이지만, 컴퓨터에서는 11111111인 -0이 나오게 되어 우리가 얻고자 하는 0과 일치하지 않는다는 결과값을 내놓을 수 있다는 것이다.

<br>

#### 2의 보수 방법
---
2의 보수 방법은 1의 보수 방법과 비슷하다. 1의 보수 방법처럼 비트를 반전(111...11 에서 음수 값을 얻고자 하는 양수를 빼는 것)시킨 후, 이에 1을 더하는 방식이다.

1의 보수 방법에 1을 더하는 방식이기에 2의 보수 방법이라 불린다.

00000111(7)의 음수 값을 2의 보수 방법으로 구하면 11111000(1의 보수 방법 기준 -7)에 1을 더한 값인 11111001로 표현이 된다.

2의 보수 방법에 대한 정의는 다음과 같다.

>총 n개의 비트로 정수를 표현할 때, 2n = 1000...0(2)에서 표현하고 싶은 음수의 절댓값을 뺀 수가 바로 2의 보수 방법으로 표현한 음수가 된다

위의 두 방식과 달리 연산에 추가적인 작업이 필요가 없고, +0과 -0을 구분하는 작업이 필요가 없어 뺄셈 연산에 2의 보수 방법이 많이 사용된다.


-참고 : https://namu.wiki/w/%EC%BB%B4%ED%93%A8%ED%84%B0%EC%97%90%EC%84%9C%EC%9D%98%20%EC%88%98%20%ED%91%9C%ED%98%84