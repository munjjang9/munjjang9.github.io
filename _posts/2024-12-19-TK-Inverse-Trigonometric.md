---
layout: post
title: 역삼각함수
author: munjjang9
tags: [Math]
date: 2024-12-19 23:00 +0900
categories: [Game Development]
toc: true
---

## 역삼각함수

원래의 삼각함수는 주기성을 띄기 때문에 일대일 대응이 아니므로 역함수의 정의가 불가능하다. 하지만 여타 함수들처럼 정의역을 제한하여 일대일 대응인 상황을 만들어준다면 이를 이용해 역함수를 정의할 수가 있다.

기본적인 역삼각함수는 이렇게 정의된다. 각 삼각함수에 역함수 표시를 해준 것과 앞에 arc가 붙는 것과 같다.

![Inverse Trigonometric](/assets/images/Inverse-Trigonometric.jpeg)

<br>

### 역삼각함수의 항등식

역삼각함수의 항등식은 다음과 같다.

![Inverse Trigonometric Identity](/assets/images/Inverse-Trigonometric-Identity.png)

<br>

### 역삼각함수의 그래프

역삼각함수의 그래프는 위에서 설명했듯이 일반적인 삼각함수의 그래프를 뒤집는 것으로는 그릴 수 없다.

역함수의 정의 자체가 일대일 대응인 경우에만 성립하기 때문에 역삼각함수에서는 삼각함수의 정의역을 제한해야만 역함수가 성립할 수 있다.

![Inverse Trigonometric Graph](/assets/images/Inverse-Trigonometric-Graph.png)

그렇기에 위처럼 그래프가 그려지는 구역이 제한되어 있다.

### 역삼각함수는 어디에 쓰일까

게임 프로그래밍에서 역삼각함수가 필요한가?라고 생각이 들 수 있다. 대표적으로 게임프로그래밍에서 역삼각함수가 쓰이는 상황은, 값이 주어졌을 때 그 값을 가지고 각을 구해야 하는 경우가 있다.

우리는 보통 삼각함수를 통해 각을 값으로 변환시켜 회전을 시키는 등의 작업을 수행한다. 그런데 반대로 회전된 값을 가지고 각을 구한다던가 하는 등의 작업을 수행해야할 경우도 생길 것이다. 그럴 때 역삼각함수가 이용된다.
